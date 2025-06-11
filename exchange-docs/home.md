# Files to IDP to SAP Integration

## Overview

This MuleSoft application provides a robust integration solution for processing files from various sources, authenticating with an Identity Provider (IDP), and sending the processed data to SAP systems.

## Architecture

The integration follows the ALC (Application Lifecycle Connectivity) methodology and implements the following flow:

1. **File Processing**: Monitors directories for incoming files (CSV, XML, JSON)
2. **Data Transformation**: Converts file content to standardized format
3. **IDP Authentication**: Authenticates with Identity Provider and retrieves access token
4. **Data Transmission**: Sends processed data to IDP endpoints
5. **SAP Integration**: Transforms IDP response and calls SAP functions
6. **File Archival**: Moves processed files to archive directory

## Features

- **Multi-format Support**: Handles CSV, XML, and JSON files
- **Robust Error Handling**: Comprehensive error handling for all integration points
- **Security**: Secure authentication with IDP and SAP systems
- **Monitoring**: Built-in logging and health check endpoints
- **Scalability**: Configurable polling intervals and batch processing
- **Environment Management**: Separate configurations for dev, test, and production

## Endpoints

### Health Check
- **GET /health**: Returns application health status

## Configuration

Environment-specific properties are managed through:
- `config-dev.properties`: Development environment
- `config-prod.properties`: Production environment

### Key Configuration Parameters

- **File System**: Input/output directories and polling frequency
- **IDP**: Host, authentication endpoints, and credentials
- **SAP**: Connection details and function mapping
- **HTTP**: Listener configuration for health checks

## Security Considerations

- Credentials are externalized using secure properties
- TLS/SSL configuration for all external communications
- Input validation and sanitization
- Comprehensive audit logging

## Monitoring and Observability

- Structured logging with correlation IDs
- Error tracking and alerting capabilities
- Performance metrics and KPIs
- File processing statistics

## Deployment

The application can be deployed to:
- CloudHub (iPaaS)
- Runtime Fabric
- On-premises Mule Runtime

## Testing

The project includes:
- MUnit test framework setup
- Sample test data
- Integration test scenarios

## Support

For questions or issues, please contact the integration team.