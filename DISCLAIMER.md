This copilot-instructions.md file is only suitable for use with VS Code + Copilot Chat.
That's because it won't affect anything and not blow up your context window to the point you'll have to pay insane amounts of money for token use.
Github Copilot is designed to work and reason in batches, after collecting the final results of a pass it summarizes those (Compaction) in its internal notes/context hierarchy. Then the working context is trimmed.

So during the investigation and preparation part of the task/project at hand, it will make heavy use of this copilot-instructions.md to deliver quality and stability, as it is planning what code to write.
After writing said code, it passes through all quality and anti-regression methodology gates to make extra sure that the design and writing phase didn't miss anything that the instructions file mandates to be checked.

Be careful - if you would load this file into another IDE/upstream AI provider, you can run into high costs. Especially soemthing like Cursor with MAX mode enabled, that would wreck your financials.
Those are designed to charge you as much as possible, so they don't use clever compaction and context editing mechanisms.

GitHub Copilot on the other hand, will really just charge you its standard $0.04 (or your quota) per premium request while you use this file in the active turn.
