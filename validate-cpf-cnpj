const ABC = [
	"a",
	"b",
	"c",
	"d",
	"e",
	"f",
	"g",
	"h",
	"i",
	"j",
	"k",
	"l",
	"m",
	"n",
	"o",
	"p",
	"q",
	"r",
	"s",
	"t",
	"u",
	"v",
	"w",
	"x",
	"y",
	"z",
];

export function validateCPFCNPJ(cpfCnpj: string) {
	const onlyDigits = cpfCnpj.replaceAll(/[./-]/g, "");
	for (let i = 0; i < 10; i++) {
		if (!onlyDigits.replaceAll(`${i}`, "").length) {
			return false;
		}
	}

	const isCpf = cpfCnpj.length <= 14;
	if (isCpf) {
		// a b c 0 0 0 a 0 c   00
		const [digits, verificationDigit] = cpfCnpj.split("-");
		const digitsArray = digits
			.replaceAll(".", "")
			.split("")
			.map((digit) => {
				if (Number.isNaN(Number.parseInt(digit))) {
					return ABC.indexOf(digit.toLowerCase()) + 17;
				}
				return Number.parseInt(digit);
			});

		const firstVerificationSum =
			11 -
			(digitsArray.reduce(
				(acc, digit, i) => acc + digit * (digitsArray.length + 1 - i),
				0,
			) %
				11);

		const firstVerification =
			firstVerificationSum > 9 ? 0 : firstVerificationSum;
		const secondVerificationSum =
			11 -
			([...digitsArray, firstVerification].reduce(
				(acc, digit, i) => acc + digit * (digitsArray.length + 2 - i),
				0,
			) %
				11);
		const secondVerification =
			secondVerificationSum > 9 ? 0 : secondVerificationSum;

		return `${firstVerification}${secondVerification}` === verificationDigit;
	}

	const [digits, verificationDigit] = cpfCnpj.split("-");
	const [block1, block2] = digits.split("/");
	const digitsArray = [
		...block1
			.replaceAll(".", "")
			.split("")
			.map((digit) => {
				if (Number.isNaN(Number.parseInt(digit))) {
					return ABC.indexOf(digit.toLowerCase()) + 17;
				}
				return Number.parseInt(digit);
			}),
		...block2.split("").map(Number),
	].reverse();

	const firstVerificationSum =
		11 -
		(digitsArray.reduce(
			(acc, digit, i) => acc + digit * ((i > 7 ? i - 8 : i) + 2),
			0,
		) %
			11);
	const firstVerification = firstVerificationSum > 9 ? 0 : firstVerificationSum;

	const secondVerificationSum =
		11 -
		([firstVerification, ...digitsArray].reduce(
			(acc, digit, i) => acc + digit * ((i > 7 ? i - 8 : i) + 2),
			0,
		) %
			11);
	const secondVerification = secondVerificationSum > 9 ? 0 : secondVerificationSum;

	return `${firstVerification}${secondVerification}` === verificationDigit;
}
