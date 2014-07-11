# NAME

Catmandu::Exporter::Table - ASCII/Markdown table exporter

# SYNOPSIS

    echo '{"one":"my","two":"table"} {"one":"is","two":"nice"}]' | \ 
    catmandu convert JSON --multiline 1 to Table
    | one | two   |
    |-----|-------|
    | my  | table |
    | is  | nice  |

    catmandu convert CSV to Table --fields id,name --header ID,Name < sample.csv
    | ID | Name |
    |----|------|
    | 23 | foo  |
    | 42 | bar  |
    | 99 | doz  |


    #!/usr/bin/env perl
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
MultiMarkdown syntax. The module delegates to [Text::MarkdownTable](https://metacpan.org/pod/Text::MarkdownTable), so
see the latter for more documentation.

# CONFIGURATION

Table output can be controlled with the options `fields`, `columns`,
`widths`, and `condense`.

See [Catmandu::Exporter](https://metacpan.org/pod/Catmandu::Exporter) for additional exporter and methods (`file`, `fh`,
`encoding`, `fix`..., `add`, `commit`...).

# SEE ALSO

[Catmandu::Exporter::CSV](https://metacpan.org/pod/Catmandu::Exporter::CSV)
