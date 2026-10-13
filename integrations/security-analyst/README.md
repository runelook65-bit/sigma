# Security Analyst — Sigma starter pack

This fork keeps the upstream rules unchanged. The manifest selects two Windows
process-creation rules at commit b4ba1f2ae16fbc0af92e7ae96364aac95bdf55b6:

- Certutil download: 19b08b1c-861d-4e75-a1ef-ea0c1baf202b (medium, test).
- Remote Mshta: b98d0db6-511d-45de-ad02-e82a98729620 (high, test).

Original authors and references remain in the YAML paths named by manifest.json.
Rules use DRL-1.1: https://github.com/SigmaHQ/Detection-Rule-License/blob/main/LICENSE.Detection.Rules.md
Match messages must retain author attribution. The Security Analyst application
also displays source/license links and original rule status.

positive-negative-cases.json defines six synthetic normalized inputs and expected
Sigma IDs (three matches, three negatives). These records are text only; no command
or URL is executed. A renamed Mshta image tests OriginalFileName matching.

The separate Security Analyst application vendors the pinned YAML files and uses a
strict allowlisted compiler. Supported fields: Image -> process_image,
OriginalFileName -> process_original_file_name, CommandLine -> command_line.
Requires platform=windows and event_type=process_start. Case-insensitive literal
equals/contains/endswith; OR lists/alternatives; AND map fields; all of selection_*.
Unsupported conditions, modifiers, wildcards and fields fail compilation.
The manifest's path names upstream paths; file names the application's vendored copy.

These files are the integration contract and test data; the runtime/compiler live
in the application, not in this repository. Keep upstream rule logic intact and
review rule updates against positive/negative cases before updating the pinned
commit. The existing upstream Mshta regression record is also tested by the app.
