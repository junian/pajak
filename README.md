## Background

Every annual tax report I always forgot the percentage **norma** value to calculate my netto from bruto income.
I usually google it and download a pdf file.
Then from there I'll just search and find my work category manually.
This is somehow frustating because searching for a keyword in pdf file make you jump from page to page until you find what you're looking for.
That's why I create this tool to filter based on search keyword.

## About

This tool is created to make lookup **Norma Perhitungan Penghasilan Netto** easier.
This netto value is used for annual tax reporting.
Very useful for self-employed, freelancer, and sole-enterpreneur working in Indonesia.

## Data extraction

The data is extracted from [PER-17/PJ/2015](http://www.pajak.go.id/sites/default/files/info-pajak/Lamp%201.pdf) pdf file.
We extract the tables using [Tabula](http://tabula.technology) and generate csv file from it.

We cleanup the csv file first by removing description rows (all rows with empty `no` column) to make the file slimmer. This is done by using `sed` command like this:

```bash
$ sed '/^"",/ d' < norma-tabula.csv > norma.csv
```

Then we add column names at the first row: **"no", "klu", "uraian", "ibukota_10", "ibukota_lain", "daerah_lain"**.

After that, the csv file is transformed to json by using [csv2josn](https://www.npmjs.com/package/csv2json) by executing this command:

```bash
$ csv2json norma.csv norma.json
```

Finally, the json data is ready to be displayed and filtered by [datatables](https://datatables.net) plugin on web page.

**Please Note** that some rows are missing because `tabula` can't extract all data from pdf tables properly. That's why several rows need to be inserted manually.

## License

The license is [Public Domain](https://github.com/junian/pajak/blob/master/LICENSE).
Do whatever you want for personal or commercial purpose, with or without attribution.
