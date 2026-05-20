# أوج (OWJ) - API Endpoints & Key Reference

## AI Providers Endpoints

| Provider | Model | Endpoint | Auth |
|----------|-------|----------|------|
| Gemini | gemini-2.0-flash | `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key={API_KEY}` | URL param |
| Groq | llama-3.3-70b-versatile | `https://api.groq.com/openai/v1/chat/completions` | Bearer token |
| BigModel | glm-4-flash | `https://open.bigmodel.cn/api/paas/v4/chat/completions` | Bearer token |
| OpenRouter | google/gemini-2.0-flash-exp:free | `https://openrouter.ai/api/v1/chat/completions` | Bearer token |
| OpenAI | gpt-4o-mini | `https://api.openai.com/v1/chat/completions` | Bearer token |
| Cerebras | llama-3.3-70b | `https://api.cerebras.ai/v1/chat/completions` | Bearer token |

## Service Endpoints

| Service | Endpoint | Method | Auth |
|---------|----------|--------|------|
| Mem0 Write | `https://api.mem0.ai/v1/memories/` | POST | Token header |
| Mem0 Read | `https://api.mem0.ai/v1/memories/?user_id=owj_user` | GET | Token header |
| Tavily Search | `https://api.tavily.com/search` | POST | API key in body |

## API Keys Storage (18 keys - embedded as defaults in app code)

### AI Providers (6)
| # | Service | Storage Key | Status |
|---|---------|-------------|--------|
| 1 | Gemini | `api_key_gemini` | embedded default |
| 2 | Groq | `api_key_groq` | embedded default |
| 3 | BigModel | `api_key_bigmodel` | embedded default |
| 4 | OpenRouter | `api_key_openrouter` | embedded default |
| 5 | OpenAI | `api_key_openai` | embedded default |
| 6 | Cerebras | `api_key_cerebras` | embedded default |

### Services (4)
| # | Service | Storage Key | Status |
|---|---------|-------------|--------|
| 7 | Mem0 | `api_key_mem0` | embedded default |
| 8 | Tavily | `api_key_tavily` | embedded default |
| 9 | Tavily MCP | `api_key_tavily_mcp` | embedded default |
| 10 | ElevenLabs | `api_key_elevenlabs` | embedded default |

### Integrations (8)
| # | Service | Storage Key | Status |
|---|---------|-------------|--------|
| 11 | GitHub | `api_key_github` | embedded default |
| 12 | Notion | `api_key_notion` | embedded default |
| 13 | YouTube | `api_key_youtube` | embedded default |
| 14 | Gmail Client ID | `api_key_gmail_client_id` | embedded default |
| 15 | Gmail Client Secret | `api_key_gmail_client_secret` | embedded default |
| 16 | Firebase API | `api_key_firebase_api` | embedded default |
| 17 | Firebase Project | `api_key_firebase_project_id` | embedded default |
| 18 | Firebase App | `api_key_firebase_app_id` | embedded default |

> **ملاحظة:** كل المفاتيح متضمنة كـ charcode arrays في `lib/core/constants.dart`
> واستخدم زر "استعادة الافتراضي" في شاشة الإعدادات عشان ترجعهم.

## Links

- **App Repo**: https://github.com/auj522005-netizen/owj-app
- **APK Download**: https://github.com/auj522005-netizen/owj-app/releases/download/v3.1.0/owj-app.apk
- **Docs Repo**: https://github.com/auj522005-netizen/owj-docs
