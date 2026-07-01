# Changelog

All notable changes to this project will be documented in this file.

## [1.0.0] - Initial Release

### Added
- **FastAPI Backend**: Robust backend structure with JWT middleware (`JWTAuthMiddleware` + `verify_student_roll`).
- **API Endpoints**: 8 API endpoints across 3 routers (`/chat`, `/analyze-doc`, `/doc/chat`, `/roadmap/*`).
- **Smart Intent Detection**: 6-category NLP classifier preventing unnecessary Gemini calls by dynamically routing requests.
- **Gemini Multi-Model Cascade**: Intelligent fallback mechanism (`gemini-2.0-flash` → `lite` → `fallback`) with exponential backoff for rate limit resilience.
- **Multi-Modal Chat**: Support for text and base64 image uploads in AI tutoring sessions.
- **Voice Chat**: Web Speech API integration with Chrome TTS featuring a keepalive workaround to prevent 15s auto-pause bugs.
- **Document Analyser**: Support for PDF, DOCX, TXT, MD, and CSV with an in-memory session store (1-hour expiry).
- **Roadmap Planner**: AI-generated study plans, offline fallback generator, 3/month plan limits, and daily task completion tracking.
- **Dual Supabase Architecture**: Split databases for Authentication (Auth DB) and Application Data (Data DB).
- **External Integrations**: Seamless connections to Maya and HOOT platforms for fetching student performance metrics.
- **Security**: Anti-inspection security shield implemented in the frontend to deter DevTools and right-clicking.
