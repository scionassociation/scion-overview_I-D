- [Notes Martin Thomson](#scion-overview)
- [Notes Juan](#notes-juan)

_________________________________________________________________________________________________________


# SCION Overview

This is the working area for the individual Internet-Draft, "SCION Overview".

* [Editor's Copy](https://scionfoundation.github.io/scion-overview_I-D/#go.draft-perrig-scion-overview.html)
* [Datatracker Page](https://datatracker.ietf.org/doc/draft-perrig-scion-overview)
* [Individual Draft](https://datatracker.ietf.org/doc/html/draft-perrig-scion-overview)
* [Compare Editor's Copy to Individual Draft](https://scionfoundation.github.io/scion-overview_I-D/#go.draft-perrig-scion-overview.diff)


## Contributing

See the
[guidelines for contributions](https://github.com/scionfoundation/scion-overview_I-D/blob/main/CONTRIBUTING.md).

Contributions can be made by creating pull requests.
The GitHub interface supports creating pull requests using the Edit (✏) button.


## Command Line Usage

Formatted text and HTML versions of the draft can be built using `make`.

```sh
$ make
```

Command line usage requires that you have the necessary software installed.  See
[the instructions](https://github.com/martinthomson/i-d-template/blob/main/doc/SETUP.md).

___________________________________________________________________________________________


# Notes Juan

For mkd examples see: https://github.com/cabo/kramdown-rfc2629
<br>
Online tool on https://ipv.sx/draftr-js/
<br>
More tools described on https://www.rfc-editor.org/pubprocess/tools/


Guidelines: https://www.ietf.org/standards/ids/guidelines/
<br>
Check .txt before submitting: https://www6.ietf.org/tools/idnits/
<br>
Submission: https://datatracker.ietf.org/submit/ \


## References:
- Paper: https://netsec.ethz.ch/publications/papers/2021_conext_deployment.pdf
- Slides: https://netsec.ethz.ch/publications/slides/2021_conext_deployment_slides.pdf
- Video: https://cloud.inf.ethz.ch/s/kgonKTDQsWxJYq2

## Proposed Automated Workflow:
- write
- `de-hyphen -$` (because copied from the PDRs there will be cut off words).
- remove citations \[[\d, ]+\]
- remove cross references,  `§`, `see`

## Standard Track Document or Not ?

According to the guidelines in
https://www.ietf.org/standards/process/informational-vs-experimental/
the SCION RFC should initially be an experimental RFC:
- 3.1 N/A because SCION is a protocol.
- 3.2 N/A because our intention is to accept comments, and change the protocol when necessary.
- 3.3 N/A because the protocol didn't start at IETF and was dropped for some reason.
- 3.4 The IETF can publish something about SCION once they know how well it works.
    - Since this is the first point that applies, the RFC should be cathegorized as Experimental.

See also [The Internet Standards Process Non-Standards Track](https://www.rfc-editor.org/rfc/rfc2026.html#section-4.2)

### Examples
Two examples of experimental RFCs are:
- [RFC1797](https://datatracker.ietf.org/doc/html/rfc1797) (very short)
- [RFC3208](https://www.rfc-editor.org/rfc/rfc3208.html)

# Details

## xml2rfc

Two relevant RFCs describing this:
- [RFC2629](https://xml2rfc.tools.ietf.org/public/rfc/html/rfc2629.html)
- [RFC7749](https://datatracker.ietf.org/doc/html/rfc7749)

_________________________________________________________________________________________________________

# How to Handle Figures

Currently, when writing in Markdown, you can only add ASCII Art figures to Internet Drafts and RFCs.
This section shortly describes how to proceed.

## Creating ASCII Art Figures

- The easiest way to create an ASCII Art figure is to use an ASCII Art editor, such as Monodraw.
- After drawing the figure in the editor, export it in text format (_.txt_).
- Save the text file with the figure in the _images_ folder of the repository.

## Inserting the Figure in the Markdown File

- Copy the ASCII art figure out of the text file.
- Paste it into the desired place in the Markdown file. 
Note to put it in-between four tildes, like this: 

~~~~
  __
<(o )___
 ( ._> /
  `---'
~~~~
