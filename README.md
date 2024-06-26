# Web of Things (WoT) Thing Description

[![Follow on Mastodon](https://img.shields.io/mastodon/follow/111609289932468076?domain=https%3A%2F%2Fw3c.social)](https://w3c.social/@wot)
[![Follow on Twitter](https://img.shields.io/twitter/follow/W3C_WoT.svg?label=follow+W3C_WoT)](https://twitter.com/W3C_WoT)
[![Stack Exchange questions](https://img.shields.io/stackexchange/stackoverflow/t/web-of-things?style=plastic)](https://stackoverflow.com/questions/tagged/web-of-things)

General information about the Web of Things can be found on https://www.w3.org/WoT/.

---

Each commit here will sync to the master, which will expose the content to http://w3c.github.io/wot-thing-description/.

For the draft TD specification for TAG review, please access this [URL](https://cdn.staticaly.com/gh/w3c/wot-thing-description/TD-TAG-review/index.html?env=dev).

To make contributions, please provide pull requests to the appropriate files,
keeping in mind that some files, most notably `index.html` and `testing/report.html`,
as well as most files under `visualization`, are
autogenerated and should not be modified directly.
See GitHub[help](https://help.github.com/articles/using-pull-requests/) for
information on how to create a pull request.

**Note (July 2023):**

**Please notice that Thing Description 1.1 is in the review phase for the Recommendation transition.
In this phase, only editorial changes (e.g., adding examples and additional explanations) and bug fixes can be applied to the [editorial draft](http://w3c.github.io/wot-thing-description/) if the whole Working Group agrees on it. Editorial changes should be labeled with 'Editorial' in the issue and corresponding PRs. New feature requests can not be considered and will be postponed to the next version of the Thing Description.**

## Thing Description Family

This repository covers the W3C Web of Things Thing Description family of specifications.

### Thing Description 1.1 (Maintenance)

- [REC](https://www.w3.org/TR/wot-thing-description11/) - Official recommendation version of the Thing Description 1.1
- [GitHub branch for the 1.1 REC](https://github.com/w3c/wot-thing-description/tree/REC1.1) - Points to the 1.1 REC tagged branch of this repository
- [errata](https://w3c.github.io/wot-thing-description/errata11.html) - Errata for version 1.1 (empty at the moment)
- [Implementation Report](https://w3c.github.io/wot-thing-description/testing/report11.html) - Implementation report of the TD 1.1 features

### Thing Description 1.0

- [REC](https://www.w3.org/TR/2020/REC-wot-thing-description-20200409/) - Official recommendation version of the Thing Description 1.0
- [GitHub branch for the 1.0 REC](https://github.com/w3c/wot-thing-description/tree/wot-td-1.0) - Branch that corresponds to the Thing Description 1.0 files
- [errata](https://w3c.github.io/wot-thing-description/errata.html) - Errata for version 1.0
- [Implementation Report](https://w3c.github.io/wot-thing-description/testing/report.html) - Implementation report of the TD 1.0 features

## Specification Rendering

Part of the document is automatically rendered using the [STTL.js](https://github.com/vcharpenay/STTL.js/) RDF template engine and Node.js.
_Any change to the document must be performed on the main HTML template [`index.template.html`](index.template.html)_, and not on `index.html`.
To render `index.html`, along with SVG figures, run:

- `npm install` to install all the dependencies
- `npm run render` to render all the files

You can also invoke the rendering script directly:

```sh
./render.sh
```

Requirements: Node.js 16, [GraphViz](https://graphviz.org/).

The script will first download and install some dependencies (triple store, Node.js dependencies) and then execute the JS script `render.js`.
The latter should always be executed within `render.sh` since it requires some env variables to be set first.

For Windows users, the script should be run in a [Cygwin shell](http://cygwin.com/). The Git package from Cygwin distribution should not be used. Alternative Git client distribution such as [Git for Windows](https://gitforwindows.org/) works better when you encounter an issue building the document using Cygwin.

### Automatic rendering

The repository is equipped with git hooks that automate the rendering process. To enable them, run `npm install` in the root folder. The hooks will render the documents automatically at every commit.
If you run the rending process manually or you do not want to execute the automatic process add the `--no-verify` option to your commit command.

### Formatting

We use Prettier for automatically formatting the files such that we have small git diffs in Pull Requests. Make sure to run `npm run format` before committing your files. If not, a GitHub action will format them by overwriting your last commit.

## Implementation Report

To generate the implementation report,
including a list of normative assertions,
issue the following command:

```sh
npm run assertions
```

A draft implementation report will be generated and output to
[testing/report.html](testing/report.html)
which will use relative links back up to [index.html](index.html).
The input to this process is [index.html](index.html)
(_not_ `index.html.template`) so make sure to execute `npm run render` first.

For this to work, the assertions need to
be marked up as in the following examples and follow RFC2119 conventions:

```html
<span class="rfc2119-assertion" id="additional-vocabularies">
  A JSON TD MAY contain additional optional vocabularies that are not in the Thing Description core model.
</span>
<span class="rfc2119-assertion" id="additional-vocabularies-prefix">
  Terms from additional optional vocabularies used in a JSON-TD MUST carry a prefix for identification within the key
  name (e.g., <tt>"http:header"</tt>).
</span>
```

The assertions must be marked up as follows:

- Enclose each assertion in a span.
- Mark the span with a unique id.
  It is recommended that the section id be followed
  by a short unique name for the specific assertion.
- Mark the span with a 'class' attribute set to `rfc2119-assertion`.
- Include one (and only one) instance of the RFC2119 keywords (MUST, MAY, etc.)
  in capitals.
  This markup does not change the rendering; it just clearly indicates
  and uniquely names the assertion.

It is strongly recommended to make assertions independent of context.
In particular, avoid using pronouns or relational expressions
referring to previous statements not included in the assertion.
Such references can always be replaced with their
antecedent ("dereferenced") without changing the meaning,
and this is less ambiguous anyway.
For example, instead of using "this serialization", use
"a JSON-TD serialization".

Also, assertions should ideally only constrain one item.
Multiple constraints should be stated in separate sentences.

Note that the above rendering process also assigns each
table entry a unique ID and these are also listed in the
table included in the implementation report.

Other data, e.g., data from test results, test specifications,
and implementation descriptions, are also needed to complete the
implementation report. See [testing/README.md](testing/README.md)
for details.

The generation of the implementation report also generates a CSS file
`testing/atrisk.css`
that highlights at-risk items in the generated `index.html`. The at-risk
items are listed in `testing/inputs/atrisk.csv`. If at-risk items are
updated, to update the at-risk highlighting the implementation report
needs to be generated first, and then the rendering.

## Resources used together with the TD Specification

In addition to the TD specification, the Working Group maintains additional resources that are relevant for implementers.
These are categorized below and their use cases explained.

### Vocabularies and Ontologies

The present specification introduces the TD Information Model as a set of constraints over different vocabularies.
The current list of vocabularies are found under [the namespaces section](https://w3c.github.io/wot-thing-description/#namespaces).

By default, if a user agent does not perform any content negotiation, a human-readable HTML documentation is returned instead of the RDF document.
To negotiate content, clients must include the HTTP header `Accept: text/turtle` in their request.

The working documents are found under the [ontology](./ontology) folder.

### Context files

In order to have reference to the TD ontology within JSON-LD documents, including TDs, we provide a JSON-LD context file.
The working document can be found at [context/td-context-1.1.jsonld](./context/td-context-1.1.jsonld) and the version-specific context file can be retrieved from the `@context` value of a TD 1.0 or TD 1.1 instance. **Note** that [context/td-context-1.1.jsonld](./context/td-context-1.1.jsonld) is the result of the rendering process and it should not be edited manually. In practice, the rendering process merges [context/td-context.jsonld](./context/td-context.jsonld), [context/json-schema-context.jsonld](./context/json-schema-context.jsonld), [context/wot-security-context.jsonld](./context/wot-security-context.jsonld), [context/hypermedia-context.jsonld](./context/hypermedia-context.jsonld).

You can find more information on how to use the context at [the Appendix of the TD specification](https://w3c.github.io/wot-thing-description/#json-ld-ctx-usage).

### JSON Schemas

We provide JSON Schema for TD and TM instances.
The working documents are found under the [validation](./validation/) folder and specific versions are linked from the Thing Description specification.
These can be used for the purposes below among others:

- TD and TM validation
- Type generation for programming languages

## Obsolete Documents

Some documents of this repository are not required to be kept in the upstream branch (main branch).
They are deleted but are recorded below with a link pointing to a tagged branch:

- Review of the main document for TAG: <https://github.com/w3c/wot-thing-description/blob/CR-request/tag-review.html>
