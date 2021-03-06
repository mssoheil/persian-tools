<h2 align="center">Persian tools</h2>

[![Build Status](https://travis-ci.org/ali-master/persian-tools.svg?branch=master)](https://travis-ci.org/ali-master/persian-tools)

PersianTools.js is a standalone, library-agnostic JavaScript that enables some of the Persian features for using in the JavaScript.

## Features

-   Convert Persian words to the number and vice versa.
-   Add and remove commas to numbers.
-   Convert Persian numbers to Arabic or English numbers and vice versa.
-   Validation of Iranian National Number(code-e Melli).
-   Get the city and province name by national code.
-   Bank number validation.
-   Get the name of the bank by bank account number.
-   Validation of the correctness of the text of the Persian language and clear the Arabic letters in the Persian text.
-   Fix Persian characters in URL.

## Getting started

There are two main ways to get PersianTools.js in your JavaScript project:
via <a href="https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_JavaScript_within_a_webpage" target="_blank">script tags</a> <strong>or</strong> by installing it from <a href="https://www.npmjs.com/" target="_blank">NPM</a>
and using a build tool like <a href="https://parceljs.org/" target="_blank">Parcel</a>,
<a href="https://webpack.js.org/" target="_blank">WebPack</a>, or <a href="https://rollupjs.org/guide/en" target="_blank">Rollup</a>.

### via Script Tag

Add the following code to an HTML file:

```html
<html>
	<head>
		<!-- Load PersianTools.js -->
		<script src="https://cdn.jsdelivr.net/npm/persian-tools2@1.1.0/dist/index.bowser.js"></script>

		<!-- Place your code in the script tag below. You can also use an external .js file -->
		<script type="text/javascript">
			// Notice there is no 'import' statement. 'all persian-tools functions like digitsEnToFa, etc...' is available on the index-page
			// because of the script tag above.

			// Takes a string made of English digits only, and returns a string that represents the same number but with Persian digits
			var convertToFa = PersianTools.digitsEnToFa(1234567);

			// etc...
		</script>
	</head>

	<body></body>
</html>
```

Open up that html file in your browser and the code should run!

### via NPM

Add PersianTools.js to your project using <a href="https://yarnpkg.com/en/" target="_blank">yarn</a> <em>or</em> <a href="https://docs.npmjs.com/cli/npm" target="_blank">npm</a>. <b>Note:</b> Because
we use ES2017 syntax (such as `import`), this workflow assumes you are using a modern browser or a bundler/transpiler
to convert your code to something older browsers understand.

```js
import * as persianTools from "persian-tools2";
// or
import { digitsEnToFa } from "persian-tools2";

// Takes a string made of English digits only, and returns a string that represents the same number but with Persian digits
const convertToFa = persianTools.digitsEnToFa(1234567);
// or
const convertToFa = digitsEnToFa(1234567);
```

## Usage

Let's take a look at what an example test case would look like using Persian-tools.

### Convert Persian words to the number and vice versa

```js
import { NumberToWords, WordsToNumber } from "persian-tools2";

WordsToNumber.convert("منفی سه هزارمین", { digits: "fa", addCommas: true }) // "-۳,۰۰۰"
WordsToNumber.convert("منفی سه هزارمین", { digits: "fa" }) // "-۳۰۰۰"
WordsToNumber.convert("منفی سه هزارمین") // -3000
WordsToNumber.convert("منفی سه هزارم") // -3000
WordsToNumber.convert("منفی سه هزار") // -3000
WordsToNumber.convert("سه هزار دویست و دوازده") // 3212
WordsToNumber.convert("دوازده هزار بیست دو") // 12022
WordsToNumber.convert("دوازده هزار بیست دو", { addCommas: true }) // "12,022"

NumberToWords.convert(500443) // "پانصد هزار و چهار صد و چهل و سه"
NumberToWords.convert("500,443") // "پانصد هزار و چهار صد و چهل و سه"
NumberToWords.convert(30000000000) // "سی میلیارد"
});
```

### Add and remove commas

```js
import { addCommas, removeCommas } from "persian-tools2";

addCommas(30000000) // "30,000,000"
addCommas(300) // "300"

removeCommas("30,000,000") // 30000000
removeCommas(300) // 300
removeCommas("300") // 300
});
```

### Convert Persian numbers to Arabic or English numbers and vice versa

```js
import { digitsArToFa, digitsArToEn, digitsEnToFa, digitsFaToEn } from "persian-tools2";

digitsArToFa("٠١٢٣٤٥٦٧٨٩"); // "۰۱۲۳۴۵۶۷۸۹"
digitsArToFa("۸۹123۴۵"); // "۸۹123۴۵"
digitsArToFa(456128); // "456128"
digitsArToFa("Text ٠١٢٣٤٥٦٧٨٩"); // "Text ۰۱۲۳۴۵۶۷۸۹"

digitsArToEn("٠١٢٣٤٥٦٧٨٩"); // "0123456789"
digitsArToEn("٨٩123٤٥"); // "8912345"
digitsArToEn(456128); // "456128"

digitsArToEn("Text ٠١٢٣٤٥٦٧٨٩"); // "Text 0123456789"

digitsEnToFa("123۴۵۶"); // "۱۲۳۴۵۶"
digitsEnToFa("٤٥٦"); // "٤٥٦"
digitsEnToFa("123۴۵۶"); // "۱۲۳۴۵۶"

digitsFaToEn("123۴۵۶"); // "123456"
digitsFaToEn("۸۹123۴۵"); // "8912345"
digitsFaToEn("۰۱۲۳۴۵۶۷۸۹"); // "0123456789"
```

### Validation of Iranian National Number(code-e Melli) and get the city and province name by that.

```js
import { verifyIranianNationalId, getPlaceByIranNationalId } from "persian-tools2";

verifyIranianNationalId("0499370899"); // true
verifyIranianNationalId("0790419904"); // true
verifyIranianNationalId("0084575948"); // true
verifyIranianNationalId("0963695398"); // true
verifyIranianNationalId("0684159414"); // true
verifyIranianNationalId("0067749828"); // true
verifyIranianNationalId("0684159415"); // false

getPlaceByIranNationalId("0499370899").city; // "شهرری"
getPlaceByIranNationalId("0790419904").city; // "سبزوار"
getPlaceByIranNationalId("0084575948").city; // "تهران مرکزی"
getPlaceByIranNationalId("0060495219").city; // "تهران مرکزی"
getPlaceByIranNationalId("0084545943").city; // "تهران مرکزی"
getPlaceByIranNationalId("0671658506").city; // "بجنورد"
getPlaceByIranNationalId("0671658506").city; // "بجنورد"
getPlaceByIranNationalId("0643005846").city; // "بیرجند"
getPlaceByIranNationalId("0906582709").city; // "کاشمر"
getPlaceByIranNationalId("0451727304").city; // "شمیران"
getPlaceByIranNationalId("0371359058").city; // "قم"
```

### Bank number validation and get the name of the bank by bank account number

```js
import { verifyCardNumber, getBankNameFromCardNumber } from "persian-tools2";

verifyCardNumber(6037701689095443); // true
verifyCardNumber(6219861034529007); // true
verifyCardNumber(6219861034529008); // false
getBankNameFromCardNumber(6037701689095443); // "بانک کشاورزی"
getBankNameFromCardNumber(6219861034529007); // "بانک سامان"
getBankNameFromCardNumber("6219861034529007"); // "بانک سامان"
```

### Validation of the correctness of the text of the Persian language and clear the Arabic letters in the Persian text.

```js
import { isPersian, toPersianChars } from "persian-tools2";

isPersian("این یک متن فارسی است؟") // true
isPersian("Lorem Ipsum Test") // false
toPersianChars("علي")) // علی
```

### Fix Persian characters in URL.

```js
import { isPersian, toPersianChars } from "persian-tools2";

URLfix(
	"https://fa.wikipedia.org/wiki/%D9%85%D8%AF%DB%8C%D8%A7%D9%88%DB%8C%DA%A9%DB%8C:Gadget-Extra-Editbuttons-botworks.js",
); // "https://fa.wikipedia.org/wiki/مدیاویکی:Gadget-Extra-Editbuttons-botworks.js"
URLfix("https://en.wikipedia.org/wiki/Persian_alphabet"); // "https://en.wikipedia.org/wiki/Persian_alphabet",
URLfix("Sample Text"); // "Sample Text"
```
