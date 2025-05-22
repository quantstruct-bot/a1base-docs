### Community & Licensing

* **Added [Code of Conduct](https://github.com/a1baseai/a1framework/blob/a5ba1b5b2166b61317d14ac080e0d3cd14856b9d/CODE_OF_CONDUCT.md)** based on Contributor Covenant v2.1 ([a5ba1b5](https://github.com/a1baseai/a1framework/commit/a5ba1b5b2166b61317d14ac080e0d3cd14856b9d))

* **Published [MIT License](https://github.com/a1baseai/a1framework/blob/f8dc6f624980e78464d58133a5ed7d48882d15e9/LICENSE)** ([f8dc6f6](https://github.com/a1baseai/a1framework/commit/f8dc6f624980e78464d58133a5ed7d48882d15e9))

* **Updated** **[CONTRIBUTING.md](https://github.com/a1baseai/a1framework/blob/a5ba1b5b2166b61317d14ac080e0d3cd14856b9d/CONTRIBUTING.md)** and **[README.md](https://github.com/a1baseai/a1framework/blob/a5ba1b5b2166b61317d14ac080e0d3cd14856b9d/README.md)** to reference new policies

### Project Reminder System (Cron)

* **Added new cron endpoint** for project reminders ([a6a806b](https://github.com/a1baseai/a1framework/commit/a6a806ba8c1cb416bbc02677ff72f4f4c8c90e69))

* Added random delay between reminder messages to avoid rate limits ([c158d53](https://github.com/a1baseai/a1framework/commit/c158d53048e4b2cc4fdbafab2f10e382dbe19c53))

* Improved logic for individual chats to fetch and use user phone numbers ([dfe161f](https://github.com/a1baseai/a1framework/commit/dfe161f5056cf3261396fa6f62408a10ad3a1321))

* ⚠️ **Authentication relaxed for MVP:** CRON_SECRET check removed ([a62a6fb](https://github.com/a1baseai/a1framework/commit/a62a6fbe3e9f1b06e9bb26e9304b3e574062df95))

### Project & Triage Logic

* **Allows multiple live projects** per user; no more excessive marking as done ([7816924](https://github.com/a1baseai/a1framework/commit/7816924ba59872421e421366c127f3660fe6a86f))

* Improved project name extraction for new projects ([bb9ef69](https://github.com/a1baseai/a1framework/commit/bb9ef694732c3c5f60bf82b9ba7d17e7515f53d8))

### Build & API Route Fixes

* Refactored route configuration for multiple API endpoints to use local config instead of shared import ([fb0807c](https://github.com/a1baseai/a1framework/commit/fb0807c5ebce9ee18c5333071c73a04f0a799da8), [fab44cd](https://github.com/a1baseai/a1framework/commit/fab44cd33f01a1d9fa4363d615cba694b692f225))

### Profile & Messaging

* Fixed WhatsApp profile image update logic ([e8976e9](https://github.com/a1baseai/a1framework/commit/e8976e9a6b91f362e0a5767868da2cd593087e3a))
