# Document Lake Releases

This repository tracks version information for Document Lake's automatic update system.

## 📦 Current Version

**Latest:** v1.2.0

See the [VERSION](VERSION) file for the current release.

## 🔔 Automatic Updates

Users running Document Lake will automatically receive update notifications when a new version is published here.

### For Users

When you see an update notification in Document Lake:

1. Click the **"Update Now"** button in the UI
2. Confirm the update in the dialog
3. Wait 2-5 minutes for automatic update
4. Done! ✨

Your data is always preserved during updates.

### Manual Update

If you prefer to update manually:

```bash
# Pull latest version
docker compose pull

# Restart services
docker compose up -d
```

## 📝 Changelog

See [CHANGELOG.md](CHANGELOG.md) for detailed release notes.

## 🚀 Quick Start

### Installation

1. Download the latest `docker-compose.yml`:
```bash
curl -O https://raw.githubusercontent.com/anbrme/document-lake-releases/main/docker-compose.yml
```

2. Start Document Lake:
```bash
docker compose up -d
```

3. Access the API:
- API: http://localhost:5001
- Elasticsearch: http://localhost:9200
- Qdrant Dashboard: http://localhost:6333/dashboard

## 🔗 Links

- **Docker Hub:** [anbrme/document-lake-api](https://hub.docker.com/r/anbrme/document-lake-api)
- **Latest Release:** [CHANGELOG.md](CHANGELOG.md)

## 📚 Features

- **Document Indexing:** Upload and index documents (PDF, DOCX, TXT, etc.)
- **Hybrid Search:** Semantic + keyword search powered by Elasticsearch
- **Local Embeddings:** Privacy-first local embedding generation
- **RAG Integration:** Vector storage with Qdrant for retrieval-augmented generation
- **Multi-tenancy:** User isolation and data privacy
- **Auto-updates:** Automatic version checking and updates

## 🔒 Privacy

- 100% local processing - no data sent to cloud
- All embeddings generated locally
- Full control over your data
- Open source and transparent

## 🐛 Issues & Support

For issues, please check:
1. [CHANGELOG.md](CHANGELOG.md) - Known issues and fixes
2. Docker logs: `docker compose logs -f api`
3. Health check: `curl http://localhost:5001/health`

## 🔐 Security

This repository only contains version information and documentation. All source code and sensitive information remains private.

---

**Auto-Update System Status:** ✅ Active

**License:** Private - Contact author for licensing information
