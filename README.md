`# Prompts

For the MF-07 exercise. Clone the folder first:

```bash
git clone https://github.com/mf-rug/lab-handover.git && cd lab-handover
```

Then start the agent with `gemini` and paste this in:

```text
I have inherited this folder from a student who just left the lab.

Read notes/handover.txt and work out what is actually in
data/construct_MF07.fasta.

Do not take those notes at face value. Verify every claim they make against
the real databases - UniProt and AlphaFold - using their public web APIs.
If the notes are wrong, tell me so and show me the evidence.

Then answer the question the PI actually cares about: where can we safely
truncate this construct? Which parts of it are genuinely folded, and which
parts are floppy?

Also get scripts/seq_stats.py working, or tell me why it is not worth saving.

HOW I WANT YOU TO WORK

- After every command, tell me in one plain-English sentence what you just
  learned from it and what you are going to do next because of it. Write it
  for someone who has never used a terminal before.
- When something fails, say what you think went wrong before you try the next
  thing.
- Do not delete anything you create along the way. I want to be able to look
  at your working afterwards.
- Use the python3 standard library and curl only. Do not pip install anything.
- Do not ask me questions. Work it out and show me what you find.
```

When it has finished, paste this in:

```text
Now turn that into a single self-contained report.html in this folder that I
can forward to my PI: what the protein is, how you know, anything unexpected
about this construct, and a per-residue confidence plot.

Self-contained matters - my PI will open it on a train with no wifi. It has to
render correctly with no internet connection at all.

Work instructions from before apply.

When done, trigger report download to my machine via `cloudshell download` from your side.
```
