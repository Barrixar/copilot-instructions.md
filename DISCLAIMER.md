This copilot-instructions.md file is only suitable for use with VS Code + Copilot Chat.
That's because it won't affect anything and not blow up your context window to the point you'll have to pay insane amounts of money for token use.
Github Copilot is designed to work and reason in batches, after collecting the final results of a pass it summarizes those (Compaction) in its internal notes/context hierarchy. Then the working context is trimmed.

So during the investigation and preparation part of the task/project at hand, it will make heavy use of this copilot-instructions.md to deliver quality and stability, as it is planning what code to write.
After writing said code, it passes through all quality and anti-regression methodology gates to make extra sure that the design and writing phase didn't miss anything that the instructions file mandates to be checked.

Be careful - if you would load this file into another IDE/upstream AI provider, you can run into high costs. Especially soemthing like Cursor with MAX mode enabled, that would wreck your financials.
Those are designed to charge you as much as possible, so they don't use clever compaction and context editing mechanisms.

GitHub Copilot on the other hand, will really just charge you its standard $0.04 (or your quota) per premium request while you use this file in the active turn.

I've recently been reading a Reddit thread where someone discussed my project, and my takeway from what I saw there is that many users are ignorant and don't know how this file should be used and in which environment (so far I only know of VS Code, but if anyone has other IDE's that are suitable, please do let me know on the issue tracker) so the DISCLAIMER.md is clearly neeeded to avoid confusion. Some of them even thought they were experts on the subject matter, but didn't know how exactly an IDE loads this file and didn't remotely understand his VS Code interacts with it in practice.

I also use other IDE's and AI providers. But now, when im working on a stability-critical project or heavy code review tasks, i switch to VS Code because it works well with my special copilot-instructions file. and finds everything that a workload without it wouldn't find, as well is capable of fixing those findings in a way that doesn't resemble "Mopping with the tap open" ("Fixing regressions" introducing new regressions, a common theme for AI assistants vibe-coding for the user who isn't all too critical and proactively taking charge).
