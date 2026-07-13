## Test environments
* local Windows 11 install, R 4.5.2
* win-builder (R-devel)

## R CMD check results

This is a new submission.

Local check (R 4.5.2, Windows): 0 errors | 0 warnings | 1 note (aside from an
environment-only PDF-manual issue explained below).

win-builder (R-devel): 0 errors | 0 warnings | 1 note.

* checking CRAN incoming feasibility ... NOTE
  New submission

## Notes on the local PDF-manual check

On the local Windows machine, `R CMD check --as-cran` additionally reported a
WARNING/ERROR while building the PDF manual. This was caused solely by the
absence of a local LaTeX installation (no `pdflatex`), not by an issue in the
package's Rd documentation:

* All 17 Rd files were confirmed to convert cleanly to LaTeX via
  `tools::Rd2latex()` (no errors or warnings).
* On win-builder (R-devel), which has a full LaTeX installation, 
  `checking PDF version of manual ... OK`, confirming the local result was an
  environment limitation rather than a package defect.

## Downstream dependencies

This is a new package; there are no reverse dependencies to check.
