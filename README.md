<div align="center">

<img src="https://github.com/user-attachments/assets/e9dbe383-db4a-405b-8fd1-9330d830938e" alt="zer0space" width="100%" />

```
███████╗██╗ ██████╗ ███████╗ ██████╗
██╔════╝██║██╔════╝ ██╔════╝██╔═████╗
███████╗██║██║  ███╗█████╗  ██║██╔██║
╚════██║██║██║   ██║██╔══╝  ████╔╝██║
███████║██║╚██████╔╝███████╗╚██████╔╝
╚══════╝╚═╝ ╚═════╝ ╚══════╝ ╚═════╝
```

**Sometimes I solve problems. Sometimes I create them.**

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=20&pause=1800&color=E5484D&center=true&vCenter=true&width=620&lines=9+Debian+nodes.+1+Docker+Swarm.;Stateless+by+constraint%2C+not+by+accident.;GitOps+or+it+didn't+happen.;Cloudflare+in+front%2C+zero+open+ports.;Building+zer0space+in+public." alt="typing" />

<br />

[![Website](https://img.shields.io/badge/zer0space.com-0D1117?style=for-the-badge&logo=cloudflare&logoColor=E5484D&labelColor=0D1117)](https://zer0space.com)
[![Dashboard](https://img.shields.io/badge/dashboard-0D1117?style=for-the-badge&logo=grafana&logoColor=E5484D&labelColor=0D1117)](https://dashboard.zer0space.com/)
[![Docs](https://img.shields.io/badge/docs-0D1117?style=for-the-badge&logo=readthedocs&logoColor=E5484D&labelColor=0D1117)](https://github.com/zer0space-net/zer0space-docs)
[![Switzerland](https://img.shields.io/badge/Switzerland-0D1117?style=for-the-badge&logo=googlemaps&logoColor=E5484D&labelColor=0D1117)](#)

</div>

---

## `~/whoami`

I build infrastructure that I then have to maintain, which keeps me honest about the decisions I make.

Most of my work lives in **[zer0space](https://github.com/zer0space-net)** — a homelab I run like production: nine machines, GitOps-managed, documented in public including the parts that aren't finished yet.

```yaml
location:  Switzerland
focus:     [ cloud, linux, automation, self-hosting, distributed-systems, ai ]
currently: making a 9-node swarm survive its own operator
motto:     "ready" is not the same as "handling traffic"
```

---

## `~/zer0space` — the ecosystem

> A documented homelab. Nine machines, stateless architecture, no open ports.

```mermaid
flowchart TD
    U([Internet]) --> CF["☁️ Cloudflare<br/>DNS · Tunnel · Access"]
    CF --> SW

    subgraph SW ["Docker Swarm — 7 nodes"]
        direction LR
        N1[node] --- N2[node] --- N3[node] --- N4[node]
    end

    SW -->|files| NFS[("📁 Central NFS<br/>external host")]
    SW -->|structured data| PG[("🐘 PostgreSQL<br/>off-cluster")]

    GH["🐙 GitHub<br/>GitOps source of truth"] -.->|deploy| SW

    classDef edge fill:#0D1117,stroke:#E5484D,stroke-width:2px,color:#fff
    classDef data fill:#161B22,stroke:#E5484D,stroke-width:2px,color:#fff
    classDef node fill:#161B22,stroke:#30363D,color:#c9d1d9
    class CF,GH edge
    class NFS,PG data
    class N1,N2,N3,N4 node
```

<details>
<summary><b>▸ Why it's built this way</b></summary>

<br />

**Stateless as an upfront constraint.** Seven Swarm nodes hold no persistent data. Files live on a central NFS mount reachable by every node; structured data lives in PostgreSQL on a separate host. Any node can be wiped and rebuilt without losing a byte.

**No exposed ports.** Cloudflare handles DNS, tunneling and authentication. Nothing is port-forwarded from the network.

**GitOps or it didn't happen.** Configuration lives in GitHub and is the source of truth. Deploys are driven from the repo — no snowflake changes on a box at 2am.

**Documented honestly.** The docs say what works *and* what doesn't. Offsite backups and restore testing are still open — writing that down is the point.

</details>

<details>
<summary><b>▸ Lessons I paid for</b></summary>

<br />

| Lesson | What it actually means |
| :-- | :-- |
| Question every component | "Does this box earn its power draw?" is a real question |
| Ready ≠ handling traffic | A green healthcheck is a claim, not a proof |
| Statelessness is a constraint | Retrofitting it costs 10× what designing for it does |
| The dangerous backup | Isn't the one that fails loudly — it's the one that lies about succeeding |

</details>

<details>
<summary><b>▸ Current status</b></summary>

<br />

```diff
+ 7-node Docker Swarm            operational
+ Central NFS storage            operational
+ PostgreSQL backend             operational
+ GitOps deployments             operational
+ Nightly backups                operational
- Offsite backups                not yet
- Restore testing                not yet
```

</details>

---

## `~/projects`

<table>
<tr>
<td width="50%" valign="top">

### 📖 [zer0space-docs](https://github.com/zer0space-net/zer0space-docs)
The architecture, the build journey, the reasoning. No configs, no secrets — just the patterns worth copying.

</td>
<td width="50%" valign="top">

### 📊 [zer0space-dashboard](https://github.com/zer0space-net/zer0space-dashboard)
`JavaScript` — the central view of the whole ecosystem. → [live](https://dashboard.zer0space.com/)

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🟢 [zer0space-status](https://github.com/zer0space-net/zer0space-status)
Public status page. Because "it's up for me" isn't monitoring.

</td>
<td width="50%" valign="top">

### 🔴 [crimson](https://github.com/zer0space-net) `client` · `backend`
Split-stack project running on the swarm.

</td>
</tr>
</table>

---

## `~/stack`

<div align="center">

**Core**

![Linux](https://img.shields.io/badge/Debian-0D1117?style=for-the-badge&logo=debian&logoColor=E5484D&labelColor=0D1117)
![Docker](https://img.shields.io/badge/Docker_Swarm-0D1117?style=for-the-badge&logo=docker&logoColor=E5484D&labelColor=0D1117)
![Python](https://img.shields.io/badge/Python-0D1117?style=for-the-badge&logo=python&logoColor=E5484D&labelColor=0D1117)
![JavaScript](https://img.shields.io/badge/JavaScript-0D1117?style=for-the-badge&logo=javascript&logoColor=E5484D&labelColor=0D1117)
![Bash](https://img.shields.io/badge/Bash-0D1117?style=for-the-badge&logo=gnubash&logoColor=E5484D&labelColor=0D1117)

**Infrastructure**

![Cloudflare](https://img.shields.io/badge/Cloudflare-0D1117?style=for-the-badge&logo=cloudflare&logoColor=E5484D&labelColor=0D1117)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-0D1117?style=for-the-badge&logo=postgresql&logoColor=E5484D&labelColor=0D1117)
![NFS](https://img.shields.io/badge/NFS-0D1117?style=for-the-badge&logo=files&logoColor=E5484D&labelColor=0D1117)
![Nginx](https://img.shields.io/badge/Nginx-0D1117?style=for-the-badge&logo=nginx&logoColor=E5484D&labelColor=0D1117)
![Git](https://img.shields.io/badge/GitOps-0D1117?style=for-the-badge&logo=github&logoColor=E5484D&labelColor=0D1117)

**AI & Automation**

![Claude](https://img.shields.io/badge/Claude_Code-0D1117?style=for-the-badge&logo=anthropic&logoColor=E5484D&labelColor=0D1117)
![Actions](https://img.shields.io/badge/GitHub_Actions-0D1117?style=for-the-badge&logo=githubactions&logoColor=E5484D&labelColor=0D1117)

</div>

---

## `~/stats`

<div align="center">

<img height="165" src="https://github-readme-stats.vercel.app/api?username=Sige0&show_icons=true&hide_border=true&bg_color=00000000&title_color=E5484D&text_color=8B949E&icon_color=E5484D&include_all_commits=true" alt="stats" />
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Sige0&layout=compact&hide_border=true&bg_color=00000000&title_color=E5484D&text_color=8B949E&langs_count=6" alt="languages" />

<br />

<img src="https://github-readme-streak-stats.herokuapp.com/?user=Sige0&hide_border=true&background=00000000&stroke=30363D&ring=E5484D&fire=E5484D&currStreakLabel=E5484D&sideLabels=8B949E&currStreakNum=8B949E&sideNums=8B949E&dates=6E7681" alt="streak" />

<br />

<img src="https://github-readme-activity-graph.vercel.app/graph?username=Sige0&bg_color=00000000&color=8B949E&line=E5484D&point=E5484D&area=true&hide_border=true" alt="activity" width="100%" />

</div>

---

<div align="center">

### `~/contact`

[![GitHub](https://img.shields.io/badge/@Sige0-0D1117?style=for-the-badge&logo=github&logoColor=E5484D&labelColor=0D1117)](https://github.com/Sige0)
[![zer0space](https://img.shields.io/badge/@zer0space--net-0D1117?style=for-the-badge&logo=github&logoColor=E5484D&labelColor=0D1117)](https://github.com/zer0space-net)
[![Web](https://img.shields.io/badge/zer0space.com-0D1117?style=for-the-badge&logo=firefoxbrowser&logoColor=E5484D&labelColor=0D1117)](https://zer0space.com)

<br />

<sub>Built on nine machines that mostly agree with each other.</sub>

<img src="https://komarev.com/ghpvc/?username=Sige0&style=flat-square&color=E5484D&label=visitors" alt="views" />

</div>
