# Angular Signal Forms: Number Inputs with `type="text"` and `inputmode`

This repository demonstrates the `number | null` binding support for `<input type="text">` introduced in Angular v21.2, and explains why `type="number"` is often the wrong choice for numeric fields.

When adding a numeric field to a Signal Form, the instinct is to reach for `<input type="number">`. It seems logical — the value is a number, so use the number input type. But MDN explicitly warns against this for fields where the spinbutton UX is not helpful, such as ages, quantities, or any number the user would never increment with arrow keys.

The problem is that `<input type="number">` gives you spinner arrows, strips leading zeros, accepts characters like `e`, `+`, and `-` (scientific notation), and can behave inconsistently across browsers and locales. For fields like age, the right approach is `<input type="text" inputmode="numeric">`, which gives you a numeric keyboard on mobile without any of those side effects.

Previously, this didn't work cleanly with Signal Forms because a `number | null` model couldn't be bound directly to a `type="text"` input — you'd have to use a custom component or workaround. As of Angular v21.2, Signal Forms handles the conversion automatically: empty input maps to `null`, valid numeric strings are parsed to numbers, and non-numeric input raises a `NativeInputParseError`.

## Features Demonstrated

- **Signal Forms**: Uses the `form()` and `FormField` APIs from `@angular/forms/signals`.
- **`number | null` on `type="text"`**: Shows how to bind a numeric model field directly to a text input using the new native support.
- **`inputmode="numeric"`**: Demonstrates the correct alternative to `type="number"` for non-incremental numeric fields.
- **Schema Validation**: Uses the built-in `min()`, `max()`, and `required()` validators to validate the numeric field in the schema rather than the template.
- **`NativeInputParseError`**: Shows how invalid (non-numeric) input is automatically surfaced as a validation error.

## Running the Demo

1. Clone the repository and install dependencies:
```bash
   npm install
```

2. Start the development server:
```bash
   npm run start
```

3. Open your browser to `http://localhost:4200`.

## Related

- [Watch the tutorial on YouTube]()
- [Signal Forms full course](https://www.udemy.com/course/angular-signal-forms/?couponCode=021409EC66FC6440B867)