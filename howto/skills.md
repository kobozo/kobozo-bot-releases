# Skills

Skills are reusable methods you own: a name, when to use them, and instructions.
Each skill has one reach. It can apply to every bot on your account, to one
project, or to one bot. A method you only want for a guided teammate stays on
that bot, and does not land in the others.

Skills are separate from the bot’s mission (the standing role in **Edit agent**).
They do not grant tools or extra permission. The message you just sent still
wins.

## Choose the reach

1. Open **My workspace → Skills**.
2. Choose **Add skill**. Fill in the name, optional **When to use**, and the
   instructions.
3. Choose the reach:
   - **All bots** — every bot of yours, including hidden ones.
   - **One project** — only tasks that run in that project. Moving a bot to
     another project drops these and picks up the new project’s skills.
   - **One bot** — only that bot, including after it moves to another project.
4. Save. A paused skill stays in the list and still counts toward the limit,
   but it is left out of the next task.

You can also open a bot and choose **Skills** (bookmark icon), or the bot menu
→ **Skills**, or add one while editing the agent. A skill added there belongs
only to that bot. Account and project skills are shown as inherited.

## Limits

- At most 6 skills for all bots, 8 per project, and 8 per bot.
- A task includes at most 8,000 characters of skill instructions. The bot’s own
  skills are kept first, then the project’s, then the account’s. Details names
  each skill that was included, and says when some were left out.
- Skills belong to your account on this server. There is no public community
  skill store. A skill is saved only after you write it or install selected
  `SKILL.md` files from a public GitHub link.
- Optional script storage is reserved for a later controlled executor. Scripts
  are not run in this version and are never sent to the model.

## Install from a Git repository

1. Open **My workspace → Skills**, or a bot’s **Skills** panel.
2. Choose **Skill from git**.
3. Paste a public GitHub link. A repository page such as
   `https://github.com/HMarzban/claude-mod` is enough. You can also paste a
   folder link (`/tree/main/skills`) or a link to one `SKILL.md` file.
4. Choose **Find skills**. Kobozo reads `SKILL.md` files only and shows the
   name, when to use, and instructions before anything is saved.
5. Choose the reach. Leave the skills you want checked and choose **Install skills**.

The saved text is a copy on this server. A later change in git does not change
the skill. Install it again if you want the new text. Hooks, plugin code and
scripts in the repository are not installed and are not run. A marketplace that
only contains hooks, such as the example above, has nothing to install until it
includes `SKILL.md` procedures.

A branch name that contains a slash is not taken from the link. Use the
repository root (its default branch) or a branch name without a slash.

## Marketplace templates

When you import a bot template that lists skills, those entries become skills
for that new bot only. They are not pasted into the mission field, and they are
not given to your other bots.

## Screenshots

Screenshot refresh: blocked in this change — capture **My workspace → Skills**
(with the three reach choices), **Skill from git** after a real preview, and a
bot’s **Skills** dialog from the demo or a safe lab install before the public
how-to publish. Do not use mockups. The marketing site at kobozo.io is a
separate repository and still needs a sentence that a skill can be copied from
a public GitHub `SKILL.md` link, plus a real screenshot, after this ships.
