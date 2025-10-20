# Document Lake - Changelog

All notable changes to Document Lake will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2025-10-20

### Fixed
- **CRITICAL:** Fixed multi-tenancy query bug where documents were not appearing in the UI
  - Changed all `user_id` term queries to use `.keyword` field for proper Elasticsearch filtering
  - Affected endpoints: `/documents`, `/search`, `/delete`, `/analyze/*`, `/documents/{id}/text`
  - Users can now see their uploaded documents correctly in Document Lake
- Fixed Elasticsearch text field queries for proper user isolation across all API endpoints

### Impact
- **Breaking Issue Fixed:** Users running v1.1.0 or earlier could not see their uploaded documents
- All documents were being stored correctly in Elasticsearch but not displayed due to query mismatch
- This release restores full document visibility and listing functionality

### Migration Notes
- **Docker Hub:** Now published to `anbrme/document-lake-api` (previously `ncdatadocker`)
- Existing data is preserved - no action needed beyond updating
- Update your `docker-compose.yml` to use `anbrme/document-lake-api:latest`

### How to Update
```bash
# Pull latest version
docker compose pull

# Restart services
docker compose up -d
```

---

## [1.1.0] - 2025-10-19

### Added
- Multi-tenancy support with user isolation
- Auto-update system via public versioning repository
- Health check endpoints for monitoring
- Batch document upload endpoint

### Changed
- Improved error handling and logging
- Enhanced Elasticsearch indexing performance

---

## [1.0.0] - 2025-10-15

### Added
- Initial release of Document Lake
- Document upload and indexing
- Hybrid search (semantic + keyword)
- Elasticsearch integration
- Local embeddings support
- Document management (delete, list, metadata updates)
- NLP analysis features (entities, classification, summarization)

---

**Note:** This is a public changelog. Detailed technical changes are tracked in the private repository.
