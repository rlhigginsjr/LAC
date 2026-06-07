# MCOC Legislative Action Center

A web-based advocacy tool that makes it simple for MOAA members to contact their elected officials on priority state and federal legislation — directly from their own email client, with no backend infrastructure, no subscriptions, and no technical expertise required by members.

**Live demo:** [rlhigginsjr.github.io/LAC](https://rlhigginsjr.github.io/LAC/)

Developed by the SE Michigan Chapter, MOAA (SEMIMOAA)** and offered freely to all state MOAA Councils.

---

## What It Does

Members visit the page and complete three steps:

1. **Enter their information** — name, address, city, ZIP, email, and MOAA chapter
2. **Select a bill** — from the current list of MCOC priority legislation
3. **Send their message** — personalized emails open pre-filled in the member's own email client (Outlook, Gmail, Apple Mail, etc.), one per legislator, ready to review and send

No data is collected. No accounts are required. Nothing is stored. The tool simply composes a personalized advocacy email and hands it off to the member's own email program to send.

---

## Current Legislation

| Bill | Title | Status |
|------|-------|--------|
| **HB 5280** ★ | Income Tax Act — retirement pay equity for NOAA & USPHS officers | **Primary target** |
| HB 5262 | Uniformity of Service Dates Act — veteran recognition | Active |
| HB 5278 | State Personal Identification Card Act — veteran ID designation | Active |
| HB 5279 | Michigan Vehicle Code — veteran driver's license designation | Active |

All four bills are referred to the **Michigan House Committee on Government Operations**.

### Committee Members Targeted

| Name | Role | Party | District |
|------|------|-------|----------|
| Rep. Brian BeGole | Chair | Republican | 71 |
| Rep. Mike Harris | Majority Vice Chair | Republican | 52 |
| Rep. John Fitzgerald | Minority Vice Chair | Democrat | 83 |
| Rep. Curtis VanderWall | Member | Republican | 102 |
| Rep. Mike McFall | Member | Democrat | 14 |

---

## How It Works (Technical)

- Single self-contained HTML file — no frameworks, no dependencies, no build step
- All bill data and legislator data live in two JavaScript arrays at the top of the script section
- Email merge fields (`[FULL_NAME]`, `[CITY]`, `[STATE]`, etc.) are replaced at runtime with what the member typed
- Each legislator button generates a `mailto:` link with the subject and body pre-populated
- A phone call script is also generated automatically at Step 3, personalized to the member

---

## Embedding on the MCOC Weebly Site

This file is hosted via GitHub Pages and embedded on the Michigan Council of Chapters website using a single iframe:

```html
<iframe src="https://YOUR-USERNAME.github.io/mcoc-action-center/"
        width="100%"
        height="950px"
        style="border:none;">
</iframe>
```

Paste that line into a Weebly **Embed Code** block on the Legislative Action page.

---

## Updating the Tool

### Adding a New Bill

Open `index.html` in any plain text editor. Find the line near the top of the `<script>` section that reads:

```javascript
const BILLS = [
```

Each bill is one entry inside that array, starting with `{` and ending with `},`. To add a new bill, paste a new entry after the last `},` and before the closing `];`.

Use this template:

```javascript
  {
    id: 5,
    code: 'HB 1234',
    priority: false,
    short: 'One-line title of the bill',
    desc: 'One or two sentences describing what the bill does. Shown on the bill selection card.',
    url: 'https://www.legislature.mi.gov/link-to-bill-text.pdf',
    subject: 'Support for HB 1234 — Short description',
    body: `Dear Representative [LAST_NAME],

Your advocacy email text goes here. Write it exactly as
you want members to send it. The fields below are replaced
automatically with what the member typed.

Respectfully,
[FULL_NAME]
[CITY], Michigan
Member, [CHAPTER]`
  },
```

**Available merge fields:**

| Field | Replaced with |
|-------|--------------|
| `[FULL_NAME]` | Member's full name |
| `[LAST_NAME]` | Legislator's last name |
| `[CITY]` | Member's city |
| `[ZIP]` | Member's ZIP code |
| `[EMAIL]` | Member's email address |
| `[ADDRESS]` | Member's street address |
| `[CHAPTER]` | Member's MOAA chapter |
| `[SALUTATION]` | Representative / Senator |

**Important:** Every entry except the very last one must end with `},` (with the comma). The final entry ends with just `}` before the closing `];`. A missing or extra comma will cause the page to go blank.

### Marking a Bill as the Primary Target

Set `priority: true` in the bill entry. This adds the gold "★ Primary target" badge to the bill card and updates the advisory note at Step 2.

### Updating Legislator Information

Find the `const LEGISLATORS = [` array in the script section. Each entry contains:

```javascript
{ 
  name: 'Full Name', 
  title: 'Role · Party · District', 
  salutation: 'Representative',   // or 'Senator'
  email: 'email@house.mi.gov', 
  phone: '(517) 000-0000' 
},
```

Update, add, or remove entries as committee membership changes.

---

## Resources

- [HB 5280 Battle Card (PDF)](https://www.moaamcoc.com/uploads/1/4/8/4/148483887/hb_5280_battle_card_r2.pdf)
- [HB 5280 One-Pager (PDF)](https://www.moaamcoc.com/uploads/1/4/8/4/148483887/michigan_house_bill_5280_-_one-pager.pdf)
- [MCOC Legislation Page](https://www.moaamcoc.com/legislation.html)
- [Michigan Legislature — Bill Search](https://www.legislature.mi.gov)

---

## Maintained By

SE Michigan Chapter,  MOAA  
Website: [semimoaa.com](https://www.semimoaa.com)

For questions about the tool or to report an issue, open a GitHub Issue in this repository.
