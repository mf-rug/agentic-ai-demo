# Agentic AI, in ten minutes

*Digital Tools in Biomolecular Sciences*

A student left the lab and handed over a folder. Somewhere in it is a protein,
and nobody is quite sure which one. You are going to hand that entire problem
to an AI agent and watch what it does.

You do not need to know any programming. You do not need to have ever used a
terminal. Nothing gets installed on your laptop.

---

## 1. Open a terminal in your browser

Go to **[shell.cloud.google.com](https://shell.cloud.google.com)** and sign in
with a Google account. You now have a real Linux computer running in a browser
tab.

## 2. Get the folder

```bash
git clone https://github.com/mf-rug/lab-handover.git && cd lab-handover
```

Have a look at what you inherited:

```bash
ls -R && cat notes/handover.txt
```

## 3. Try it the old way first — 30 seconds

The previous student left a script behind and swore it worked:

```bash
python3 scripts/seq_stats.py
```

Read what comes back. **For someone who does not code, this is normally where
the project ends.** Do not try to fix it. Just notice how you feel.

## 4. Hand the whole problem over

```bash
gemini
```

Then paste in this prompt:

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

Now **read every step before you approve it**, and approve them one at a time.

## 5. Ask for something you can send to your PI

When it has finished, paste this in:

```text
Now turn that into a single self-contained report.html in this folder that I
can forward to my PI: what the protein is, how you know, anything unexpected
about this construct, and a per-residue confidence plot.

Self-contained matters - my PI will open it on a train with no wifi. It has to
render correctly with no internet connection at all.
```

Then look at what it made:

```bash
python3 -m http.server 8080
```

Click **Web Preview** (the eye icon, top right) → *Preview on port 8080* →
open `report.html`. Press `Ctrl+C` in the terminal when you are done.

---

## What to watch for

This is the actual point of the exercise.

1. **It opens files you never mentioned.** You pointed it at a folder, not a
   file list. It decided what was worth reading.
2. **It runs things, and they fail.** Then it reads the error and tries
   something else. Nobody copy-pastes the error message for it.
3. **It checks a claim instead of believing it.** The handover notes state
   something as fact. Watch whether the agent takes that on trust.
4. **It notices something nobody asked about.** There is a detail in this
   construct that is not in the notes and not in the prompt. See if it finds
   it — and whether it works out why it matters.

## Why you are clicking "allow" on every step

That prompt is not a formality, and it is not there to slow you down. It is the
only thing standing between a confident agent and your files. An agent that can
read, write and execute is exactly as dangerous as it is useful, and the person
reading each command before approving it is the entire safety model.

So read them. It is also the best free lesson in shell commands you will get.

## The comparison that matters

You have probably already used ChatGPT to write a bit of code. That workflow is:

> ask → read the answer → paste it → it breaks → paste the error back → repeat

You are the hands, the eyes, and the error handler. Every loop goes through you,
which means every loop needs *you* to understand roughly what is going on.

What you just watched is the same kind of model with three extra abilities: it
can **look** at your actual files, **run** commands, and **see the output** — so
it closes that loop itself. It is not more intelligent. It is *connected*.

That is the whole difference, and it is why the useful question is no longer
"can I write this?" but **"can I tell whether this is right?"**

---

## Now check its work

The agent is fluent, fast, and completely confident — including when it is
wrong. Start here:

**Did it actually do what it said?** You asked for a report that works with no
internet. Check:

```bash
grep -o 'src="http[^"]*"' report.html
```

Every line that comes back is a file your PI's browser has to download from
somewhere else. If anything appears, the report is *not* self-contained — no
matter what the agent told you. This is not a hypothetical: when we tested this
exercise, one agent loaded its plotting library from the internet and then
reported that it had produced a self-contained file.

Then keep going:

- Every database claim should come with an accession number. Follow one. Does
  it land on the entry the agent says it does?
- Does the confidence plot actually match what the text claims about it?
- If it contradicted the handover notes: is *it* right, or are the notes?

Checking that is now your job, and it is the part of your degree that does not
get automated.

## If you finish early

Paste these in, one at a time:

- `That report is not self-contained. Fix it, and this time verify it yourself before telling me it is done.`
- `Add an interactive 3D view of the structure, coloured by confidence, with the unexpected residue highlighted.`
- `Rewrite the report for my PI, who is a biologist and does not code.`
- `What would be different if the handover notes had been right?`
- `Design primers to make the construct you are recommending.`
