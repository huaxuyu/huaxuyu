# Yu Lab Website

This repository now contains the Vue website for Yu Lab, a clinical
metabolomics and open-source software lab at the First Affiliated Hospital of
Zhejiang University School of Medicine.

## Development

- [Google Scholar](https://scholar.google.ca/citations?user=tQAb4wkAAAAJ&hl=en)
- Email: huaxuyu@zju.edu.cn | yhxchem@outlook.com
- Personal website: [https://huaxuyu.github.io/huaxuyu/](https://huaxuyu.github.io/huaxuyu/)

Install dependencies and start the local site:

```bash
npm install
npm run dev
```

Build the production site:

```bash
npm run build
```

Preview the production build locally:

```bash
npm run preview
```

The app uses hash-based tab navigation and `base: "./"` in `vite.config.js`, so
the build works on GitHub Pages whether it is served from a project URL first or
from the future custom domain `huaxuyulab.com`.
