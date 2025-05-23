# 前端架構師／前端架構核心工作清單

## 1. 專案骨架與模組化設計
| 做什麼 | 為什麼要做 | 常見產出 |
|--------|------------|----------|
| 決定資料夾結構、路由規劃、共用元件層級 (Atoms/Molecules/Organisms) | 讓多人協作時檔案不打架，減少 PR 衝突 | `apps/`、`packages/`、元件命名規範、README |

## 2. 技術選型與基礎建置
| 做什麼 | 為什麼要做 | 常見產出 |
|--------|------------|----------|
| 選擇框架（React、Vue）、TypeScript、打包工具（Vite、Webpack）、CSS 方案（Tailwind、CSS-in-JS） | 影響維護成本與學習曲線 | Tech Stack 決策文件、Boilerplate 範例專案 |

## 3. 性能優化策略
| 做什麼 | 為什麼要做 | 常見產出 |
|--------|------------|----------|
| Lazy Load、Code Splitting、SSR/SSG、瀑布流優化、圖片壓縮 | 降低首屏時間、提升 SEO、增加轉換率 | Lighthouse 報表、webpack bundle analyzer 報告 |

## 4. 狀態管理與資料流
| 做什麼 | 為什麼要做 | 常見產出 |
|--------|------------|----------|
| 設計全域與區域狀態 (Redux, Zustand, React Query)、定義 API Contract | 避免 prop-drilling、確保 API 變動能快速回應 | Swagger/Spec 文件、型別定義 (`*.d.ts`)、Hooks 範例 |

## 5. 設計系統與可及性 (A11y)
| 做什麼 | 為什麼要做 | 常見產出 |
|--------|------------|----------|
| 規範色彩、字體、Icon、Spacing；建立可重用 UI Library | 保持品牌一致、降低重工 | Figma Token、Storybook、Component Docs |

## 6. 自動化測試與品質把關
| 做什麼 | 為什麼要做 | 常見產出 |
|--------|------------|----------|
| Unit (Jest)、E2E (Playwright/Cypress)、Lint/Format | 早期抓 Bug、確保重構安全 | CI badge、coverage 報表、Git pre-commit hook |

## 7. CI/CD 與佈署流程
| 做什麼 | 為什麼要做 | 常見產出 |
|--------|------------|----------|
| 建 Git Flow、PR 規範，撰寫 GitHub Actions/GitLab CI pipeline | 自動化測試 → 打包 → 部署，減少人工失誤 | `.gitlab-ci.yml` / `.github/workflows/**`、環境變數管理 |

## 8. 安全與合規
| 做什麼 | 為什麼要做 | 常見產出 |
|--------|------------|----------|
| Content Security Policy、XSS/CSRF 防護、依地區法規（GDPR） | 保護使用者資料、避免罰款 | SecOps Checklist、Security Headers 設定 |

## 9. 監控與可觀測性
| 做什麼 | 為什麼要做 | 常見產出 |
|--------|------------|----------|
| 前端 Log、Error Tracking (Sentry)、Real User Monitoring | 及時掌握線上錯誤與性能 | Kibana Dashboards、Sentry Alert 設定 |

## 10. 文件與知識傳承
| 做什麼 | 為什麼要做 | 常見產出 |
|--------|------------|----------|
| 撰寫開發指南、部署手冊、決策紀錄 (ADR) | 新人 onboarding 快、決策有跡可循 | Confluence / Notion / Markdown Docs |

---

#### 核心思維小結
1. **標準化**：把「大家都要做」的步驟寫成腳本或 CI，多人協作才不會發散。  
2. **可維護**：每一個技術選擇都要考量 6 個月後的自己是否看得懂。  
3. **量化**：用指標（Lighthouse 分數、Error Rate）衡量成效，才能說服老闆與團隊。  
4. **自動化**：重複動作就寫腳本，省下的是未來好幾天的人力。  
