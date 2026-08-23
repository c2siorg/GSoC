# Complete Neural Network Design Studio for TensorMap

# Project Abstract

TensorMap is a visual neural network design platform that enables users to build, train, and analyze machine learning models through an intuitive drag-and-drop interface. This GSoC 2026 project transformed TensorMap from a basic prototype with 4 hardcoded layer types into a production-ready neural network design studio with 15 layer types, real-time training visualization, multi-format model export, comprehensive interpretability tools, and automated hyperparameter tuning capabilities.

## [GSoC Project Page](https://github.com/c2siorg/tensormap/issues/120)

## [GSoC Project Proposal](https://docs.google.com/document/d/12BlvLQIq_cF9XhMi6GW5VBXqS41cDgfx/edit?usp=sharing&ouid=104407836869452070788&rtpof=true&sd=true)

## [GitHub Organization Repo](https://github.com/c2siorg/tensormap)

## [GitHub Personal Repo](https://github.com/kartikeyg0104)

## [Commits during GSoC 2026](https://github.com/c2siorg/tensormap/pulls?q=is%3Apr+author%3Akartikeyg0104+is%3Amerged)

## [Project Wiki](https://github.com/c2siorg/tensormap)

## [GSoC Blog](https://medium.com/@kartikeygupta_/google-summer-of-code-2026-final-work-product-submission-9c8996ef585b)

# Work Summary

Over 12 weeks, I successfully completed all 6 planned phases of the TensorMap transformation project, delivering:

- **Phase 1 (Weeks 1-3): Foundation Infrastructure** - Established CI/CD pipeline with GitHub Actions, created registry-driven layer architecture, and built comprehensive test infrastructure (pytest + vitest)
- **Phase 2 (Weeks 2-3): Layer Expansion** - Extended from 4 to 15 layer types covering CNNs, RNNs, regularization layers, and implemented GenericLayerNode component with categorized sidebar
- **Phase 3 (Weeks 4-6): Training Visualization** - Built persistent training job system with Socket.IO room isolation, real-time loss/accuracy charts, and cooperative cancellation mechanism
- **Phase 4 (Weeks 7-8): Model Export** - Implemented multi-format export system (SavedModel, TFLite, ONNX) with automatic storage management and model metadata endpoints
- **Phase 5 (Weeks 9-10): Interpretability** - Created comprehensive analysis dashboard with confusion matrices, feature importance, prediction explorer, and async computation patterns
- **Phase 6 (Weeks 11-12): Hyperparameter Tuning** - Built grid and random search engine with sequential trial execution, real-time progress streaming, and one-click parameter application

**Key Metrics:**
- 13 merged pull requests
- ~15,000 lines of production code
- ~8,000 lines of comprehensive tests
- 580+ tests passing (425 backend + 155 frontend)
- 100% CI/CD success rate
- All deliverables completed ahead of schedule

# What Covered

## ✅ Visual Layer Builder (15 Layer Types)
- Core layers: Input, Dense, Flatten
- Convolutional: Conv2D
- Pooling: MaxPooling2D, AveragePooling2D, GlobalAveragePooling2D
- Recurrent: LSTM, GRU, SimpleRNN
- Encoding: Embedding
- Regularization: Dropout, BatchNormalization
- Utility: Reshape, Concatenate
- GenericLayerNode component with category-based color coding
- Categorized sidebar for easy discovery
- Dynamic parameter configuration panels

## ✅ Real-Time Training System
- Persistent training jobs with full state machine (PENDING → RUNNING → COMPLETED/FAILED/CANCELLED)
- Live loss & accuracy charts using Recharts
- Socket.IO per-job rooms for isolated streaming
- Training progress header with ETA calculation
- Metrics summary bar showing best epoch performance
- Interactive Stop Training button with cooperative cancellation
- Crash recovery system marking orphaned jobs as FAILED
- Structured per-epoch metric persistence via MetricsCallback

## ✅ Model Export & Storage Management
- Multi-format export: SavedModel (TensorFlow native), TFLite (mobile/edge), ONNX (cross-framework)
- Export status tracking and polling
- Automatic storage management with configurable GB limits
- Hourly cleanup loop for expired exports
- Model architecture metadata endpoint with parameter count estimation
- Fixed critical model deletion CASCADE bug

## ✅ Post-Training Analysis & Interpretability
- Confusion matrix with interactive heatmap visualization
- Classification report with color-coded metrics (precision, recall, f1-score)
- Permutation feature importance using async 202/200 polling pattern
- Prediction explorer with pagination, sorting, and confidence filtering
- Residual plots for regression models
- Task-type routing (classification vs. regression)
- All computations non-blocking via asyncio.to_thread()

## ✅ Hyperparameter Tuning Engine
- Grid search with Cartesian product generation (max 50 combinations)
- Random search supporting 3 spec types: discrete, uniform, log_uniform
- Sequential trial execution with 600s timeout per trial
- Early stopping support with configurable thresholds
- Duration estimation using training history
- Socket.IO real-time progress streaming
- TuningConfigForm with client-side validation
- TuningProgressPanel with live results table and best trial highlighting
- ApplyBestBanner for one-click parameter application

## ✅ Infrastructure & Quality
- GitHub Actions CI/CD pipeline with PostgreSQL test containers
- 425+ backend tests (pytest) and 155+ frontend tests (vitest)
- Registry-driven architecture reducing layer addition from 6+ files to 1 entry
- Type-safe throughout (Pydantic + TypeScript)
- Comprehensive error handling and resource cleanup
- Accessible UI (WCAG 2.1 AA compliance)
- Complete documentation (API, integration, troubleshooting)

## 🔧 Technical Innovations
- **Per-job Socket.IO rooms** solving multi-tenant isolation challenges
- **Dual-write/dual-read migration** enabling zero-downtime schema changes
- **Registry pattern** eliminating hardcoded if/elif chains
- **Async 202/200 polling pattern** for long-running computations
- **Cooperative cancellation** at epoch boundaries preventing resource leaks

# What left

All planned GSoC 2026 goals were successfully completed. The project is production-ready with comprehensive test coverage and documentation.

## 🔮 Potential Future Enhancements (Post-GSoC)

While all objectives were achieved, the extensible architecture provides opportunities for community contributions:

### Advanced Analytics
- Convergence plots showing hyperparameter search progress
- Training curve comparison across multiple models
- Statistical significance testing for hyperparameter differences
- Automated anomaly detection in training metrics

### Expanded ML Support
- Additional layer types (Attention, Transformer blocks, Custom layers)
- AutoML support (NAS, AutoKeras integration)
- Distributed training support
- Model versioning and experiment tracking

### User Experience
- Internationalization (i18n) for global accessibility
- Keyboard shortcuts for power users
- Template gallery for common architectures
- Collaborative editing (multi-user workspaces)

### Enterprise Features
- Role-based access control (RBAC)
- Model registry with governance
- API key management
- Audit logs and compliance tracking

---

**Contributor:** Kartikey Gupta  
**Email:** kartikeyf12@gmail.com  
**GitHub:** [@kartikeyg0104](https://github.com/kartikeyg0104)  
**Organization:** C2SI (Ceylon Computer Science Institute)  
**Mentors:** Oshan Mudannayake (Ivantha)
