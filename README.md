# NAME

Catmandu::Exporter::Table - ASCII/Markdown table exporter

# STATUS

[![Build Status](https://travis-ci.org/LibreCat/Catmandu-Exporter-Table.png)](https://travis-ci.org/LibreCat/Catmandu-Exporter-Table)
[![Coverage Status](https://coveralls.io/repos/LibreCat/Catmandu-Exporter-Table/badge.png)](https://coveralls.io/r/LibreCat/Catmandu-Exporter-Table)
[![Kwalitee Score](http://cpants.cpanauthors.org/dist/Catmandu-Exporter-Table.png)](http://cpants.cpanauthors.org/dist/Catmandu-Exporter-Table)

# SYNOPSIS

With [catmandu](https://metacpan.org/pod/catmandu) command line client:

    echo '{"one":"my","two":"table"} {"one":"is","two":"nice"}' | \ 
    catmandu convert JSON --multiline 1 to Table
    | one | two   |
    |-----|-------|
    | my  | table |
    | is  | nice  |

    catmandu convert CSV to Table --fields id,name --columns ID,Name < sample.csv
    | ID | Name |
    |----|------|
    | 23 | foo  |
    | 42 | bar  |
    | 99 | doz  |

In Perl scripts:

    use Catmandu::Exporter::Table;
    my $exp = Catmandu::Exporter::Table->new;
    $exp->add({ title => "The Hobbit", author => "Tolkien" });
    $exp->add({ title => "Where the Wild Things Are", author => "Sendak" });
    $exp->add({ title => "One Thousand and One Nights" });
    $exp->commit;

    | author  | title                       |
    |---------|-----------------------------|
    | Tolkien | The Hobbit                  |
    | Sendak  | Where the Wild Things Are   |
    |         | One Thousand and One Nights |

# DESCRIPTION

This [Catmandu::Exporter](https://metacpan.org/pod/Catmandu::Exporter) exports data in tabular form, formatted in
MultiMarkdown syntax.

The output can be used for simple display, for instance to preview Excel files
on the command line. Use [Pandoc](http://johnmacfarlane.net/pandoc/) too
further convert to other table formats, e.g. `latex`, `html5`, `mediawiki`:

    catmandu convert XLS to Table < sheet.xls | pandoc -t html5

By default columns are sorted alphabetically by field name.

# CONFIGURATION

Table output can be controlled with the options `fields`, `columns`,
`widths`, and `condense` as documented in [Text::MarkdownTable](https://metacpan.org/pod/Text::MarkdownTable). 

- file
- fh
- encoding
- fix

    Standard options of [Catmandu:Exporter](Catmandu:Exporter)

- condense

    Write table in condense format with unaligned columns.

- fields

    Field names as comma-separated list or array reference.

- columns

    Column names as comma-separated list or array reference. By default field
    names are used as column names.

- header

    Include header lines. Enabled by default.

- widths

    Column widths as comma-separated list or array references. Calculated from all
    rows by default. Long cell values can get truncated with this option.

- schema

    Supply fields and (optionally) columns in a [JSON Table
    Schema](http://dataprotocols.org/json-table-schema/) as JSON file or hash
    reference having the following structure:

        {
          "fields: [
            { "name": "field-name-1", "title": "column title 1 (optional)" },
            { "name": "field-name-2", "title": "column title 2 (optional)" },
            ...
          ]
        }

# METHODS

See [Catmandu::Exporter](https://metacpan.org/pod/Catmandu::Exporter) 

# SEE ALSO

This module is based on [Text::MarkdownTable](https://metacpan.org/pod/Text::MarkdownTable).

Similar Catmandu Exporters for tabular data include
[Catmandu::Exporter::CSV](https://metacpan.org/pod/Catmandu::Exporter::CSV), [Catmandu::Exporter::XLS](https://metacpan.org/pod/Catmandu::Exporter::XLS), and
[Catmandu::Exporter::XLSX](https://metacpan.org/pod/Catmandu::Exporter::XLSX).
