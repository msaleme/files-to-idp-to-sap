# Files to IDP to SAP Integration

![MuleSoft](https://img.shields.io/badge/MuleSoft-4.4.0-blue)
![SAP](https://img.shields.io/badge/SAP-Integration-green)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

## 🚀 Overview

Enterprise-grade MuleSoft integration solution that seamlessly processes files from various sources, authenticates with Identity Provider (IDP) systems, and transmits data to SAP environments. Built following Application Lifecycle Connectivity (ALC) methodology for robust, scalable, and maintainable integration patterns.

## 🏗️ Architecture

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   File      │    │   MuleSoft  │    │     IDP     │    │     SAP     │
│  Sources    │───▶│ Integration │───▶│ Auth & API  │───▶│   System    │
│ (CSV/XML/   │    │   Platform  │    │             │    │             │
│  JSON)      │    │             │    │             │    │             │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
```

## ✨ Features

### 🔄 **Multi-Format Processing**
- **CSV**: Intelligent parsing with configurable delimiters
- **XML**: Schema validation and transformation
- **JSON**: Structure validation and normalization

### 🔐 **Security & Authentication**
- OAuth 2.0 integration with IDP systems
- Secure credential management
- TLS/SSL encrypted communications
- Role-based access control

### 🛡️ **Robust Error Handling**
- Comprehensive error classification
- Automatic retry mechanisms
- Circuit breaker patterns
- Detailed audit logging

### 📊 **Monitoring & Observability**
- Real-time processing metrics
- Health check endpoints
- Correlation ID tracking
- Performance analytics

### 🌍 **Environment Management**
- Development, staging, and production configurations
- Externalized property management
- Environment-specific deployment

## 🏢 Enterprise Integration Patterns

| Pattern | Implementation | Use Case |
|---------|----------------|----------|
| **File-to-API** | File listener → DataWeave → HTTP | Real-time file processing |
| **Batch Processing** | Scheduled polling → Batch aggregation | Large volume handling |
| **Error Recovery** | DLQ + Retry logic | Fault tolerance |
| **Circuit Breaker** | Timeout + Fallback | System resilience |

## 🛠️ Technical Stack

- **Runtime**: MuleSoft 4.4.0
- **Language**: DataWeave 2.0
- **Testing**: MUnit Framework
- **Build**: Maven 3.x
- **Deployment**: CloudHub / Runtime Fabric
- **Monitoring**: Anypoint Monitoring

## 📁 Project Structure

```
files-to-idp-to-sap/
├── src/
│   ├── main/
│   │   ├── mule/
│   │   │   ├── global-config.xml          # Global configurations
│   │   │   ├── error-handlers.xml         # Error handling strategies
│   │   │   └── files-to-idp-to-sap.xml   # Main integration flows
│   │   └── resources/
│   │       ├── config-dev.properties      # Development config
│   │       ├── config-prod.properties     # Production config
│   │       └── log4j2.xml                # Logging configuration
│   └── test/
│       ├── munit/                         # Unit tests
│       └── resources/
├── exchange-docs/
│   └── home.md                           # Exchange documentation
├── pom.xml                               # Maven configuration
└── mule-artifact.json                   # Mule artifact descriptor
```

## 🚀 Quick Start

### Prerequisites

- **MuleSoft Anypoint Studio** 7.x or higher
- **Java** 8 or 11
- **Maven** 3.6+
- **SAP JCo Libraries** (for SAP connectivity)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/msaleme/files-to-idp-to-sap.git
   cd files-to-idp-to-sap
   ```

2. **Configure environment properties**
   ```bash
   cp src/main/resources/config-dev.properties.template src/main/resources/config-dev.properties
   # Edit configuration values
   ```

3. **Install dependencies**
   ```bash
   mvn clean install
   ```

4. **Run the application**
   ```bash
   mvn mule:run
   ```

## ⚙️ Configuration

### Environment Properties

#### File System Configuration
```properties
# File processing settings
file.input.dir=/path/to/input
file.archive.dir=/path/to/archive
file.polling.frequency=30
```

#### IDP Configuration
```properties
# Identity Provider settings
idp.host=your-idp-host.com
idp.auth.path=/oauth/token
idp.data.path=/api/v1/data
```

#### SAP Configuration
```properties
# SAP system settings
sap.host=sap-server.company.com
sap.system.number=00
sap.client=100
sap.username=${secure::sap.username}
sap.password=${secure::sap.password}
```

### Secure Properties

Store sensitive information using Anypoint Platform's secure properties:

```bash
# Set secure properties
anypoint-cli secure-properties set sap.username "your-username"
anypoint-cli secure-properties set sap.password "your-password"
anypoint-cli secure-properties set idp.client.secret "your-secret"
```

## 🔄 Integration Flows

### 1. File Processing Flow
- **Trigger**: File listener on input directory
- **Processing**: Format detection and parsing
- **Validation**: Schema and business rule validation
- **Transformation**: DataWeave transformation to standard format

### 2. IDP Authentication Flow
- **OAuth Flow**: Client credentials grant
- **Token Management**: Automatic token refresh
- **API Calls**: Authenticated data transmission

### 3. SAP Integration Flow
- **RFC Calls**: Direct SAP function calls
- **BAPI Integration**: Business API interactions
- **Error Handling**: SAP-specific error management

## 📊 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | GET | Application health status |
| `/metrics` | GET | Performance metrics |
| `/process-file` | POST | Manual file processing trigger |

## 🧪 Testing

### Unit Tests
```bash
# Run MUnit tests
mvn test

# Run with coverage
mvn clean test -Dmunit.coverage
```

### Integration Tests
```bash
# Run integration test suite
mvn verify -Pintegration-tests
```

### Performance Tests
```bash
# Load testing with sample data
mvn verify -Pperformance-tests
```

## 📈 Monitoring & Observability

### Health Checks
```bash
curl http://localhost:8081/health
```

### Metrics Endpoint
```bash
curl http://localhost:8081/metrics
```

### Log Analysis
- **Correlation IDs**: Track requests across systems
- **Structured Logging**: JSON format for easy parsing
- **Error Classification**: Categorized error types

## 🚀 Deployment

### CloudHub Deployment
```bash
# Deploy to CloudHub
mvn clean package deploy -DmuleDeploy \
  -Dcloudhub.application=files-to-idp-to-sap \
  -Dcloudhub.environment=production \
  -Dcloudhub.worker.type=Small \
  -Dcloudhub.workers=1
```

### Runtime Fabric Deployment
```bash
# Deploy to Runtime Fabric
mvn clean package deploy -DmuleDeploy \
  -Drtf.application=files-to-idp-to-sap \
  -Drtf.target=production-rtf \
  -Drtf.replicas=2
```

## 🔧 Troubleshooting

### Common Issues

#### File Processing Issues
```bash
# Check file permissions
ls -la /path/to/input/
# Verify polling configuration
grep "polling.frequency" src/main/resources/config-*.properties
```

#### IDP Authentication Failures
```bash
# Test IDP connectivity
curl -X POST https://your-idp-host.com/oauth/token \
  -H "Content-Type: application/json" \
  -d '{"client_id":"your-client-id","client_secret":"your-secret"}'
```

#### SAP Connection Issues
```bash
# Verify SAP connectivity
telnet sap-server.company.com 3300
# Check SAP user permissions
```

## 📚 Documentation

- [Exchange Documentation](./exchange-docs/home.md)
- [API Specification](./api/files-to-idp-to-sap.raml)
- [DataWeave Transformations](./docs/dataweave-examples.md)
- [Error Handling Guide](./docs/error-handling.md)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow MuleSoft best practices
- Write comprehensive tests
- Update documentation
- Use semantic commit messages

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Issues**: [GitHub Issues](https://github.com/msaleme/files-to-idp-to-sap/issues)
- **Documentation**: [Project Wiki](https://github.com/msaleme/files-to-idp-to-sap/wiki)
- **Community**: [MuleSoft Community](https://forums.mulesoft.com/)

## 📞 Contact

- **Author**: [msaleme](https://github.com/msaleme)
- **Email**: support@company.com
- **LinkedIn**: [Connect with us](https://linkedin.com/company/yourcompany)

---

**Built with ❤️ using MuleSoft Anypoint Platform**

*This integration solution follows enterprise-grade patterns and is production-ready for mission-critical business processes.*