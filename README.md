Country Separators JSON
This repository contains a JSON file (countries_separators.json) with information about countries, their ISO 2-character codes, thousand separators, and decimal separators.

File Contents
The countries_separators.json file includes an array of objects, each representing a country. Each object has the following properties:

country: The name of the country.
iso_code: The ISO 2-character code for the country.
thousand_separator: The symbol used for thousand separators in that country.
decimal_separator: The symbol used for decimal separators in that country.
Example entry:

json
Code kopieren
{
    "country": "United States",
    "iso_code": "US",
    "thousand_separator": ",",
    "decimal_separator": "."
}
How to Use
Loading the JSON File
You can load and use the JSON file in various programming languages. Below are examples in JavaScript and Python.

JavaScript
Using Node.js to read and parse the JSON file:

javascript
Code kopieren
const fs = require('fs');

// Read the JSON file
fs.readFile('countries_separators.json', 'utf8', (err, data) => {
    if (err) {
        console.error(err);
        return;
    }

    // Parse JSON data
    const countries = JSON.parse(data);

    // Example: Print all countries and their separators
    countries.forEach(country => {
        console.log(`Country: ${country.country}, Thousand Separator: ${country.thousand_separator}, Decimal Separator: ${country.decimal_separator}`);
    });
});
Python
Using Python to read and parse the JSON file:

python
Code kopieren
import json

# Read the JSON file
with open('countries_separators.json', 'r') as file:
    countries = json.load(file)

# Example: Print all countries and their separators
for country in countries:
    print(f"Country: {country['country']}, Thousand Separator: {country['thousand_separator']}, Decimal Separator: {country['decimal_separator']}")
Integrating with Your Application
You can integrate this JSON file into your application to format numbers according to the conventions of different countries. This can be useful for internationalization (i18n) purposes.

Example Usage
JavaScript
javascript
Code kopieren
function formatNumber(number, country) {
    // Find the country object by ISO code or name
    const countryInfo = countries.find(c => c.iso_code === country || c.country === country);
    if (!countryInfo) {
        throw new Error('Country not found');
    }

    const { thousand_separator, decimal_separator } = countryInfo;

    // Format the number using the country's separators
    return number.toLocaleString('en-US', {
        useGrouping: true,
        minimumFractionDigits: 2,
        maximumFractionDigits: 2
    }).replace(/,/g, thousand_separator).replace(/\./g, decimal_separator);
}

// Example: Format a number for Germany
const formattedNumber = formatNumber(1234567.89, 'DE');
console.log(formattedNumber); // "1.234.567,89"
Python
python
Code kopieren
def format_number(number, country_code):
    # Find the country object by ISO code
    country_info = next((c for c in countries if c['iso_code'] == country_code), None)
    if not country_info:
        raise ValueError('Country not found')

    thousand_separator = country_info['thousand_separator']
    decimal_separator = country_info['decimal_separator']

    # Format the number using the country's separators
    formatted_number = f"{number:,.2f}".replace(',', 'X').replace('.', decimal_separator).replace('X', thousand_separator)
    return formatted_number

# Example: Format a number for Germany
formatted_number = format_number(1234567.89, 'DE')
print(formatted_number)  # "1.234.567,89"
Contributing
If you find any inaccuracies or want to add more countries, feel free to open a pull request. Contributions are welcome!

License
This project is licensed under the MIT License.

Acknowledgements
The data in this JSON file is compiled from various sources to provide accurate and up-to-date information on country-specific number formatting conventions.
