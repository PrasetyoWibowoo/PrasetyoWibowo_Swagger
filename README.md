# API Testing Web Project with Swagger

A comprehensive web application for testing and documenting REST API endpoints using Swagger/OpenAPI specification. This project provides an interactive interface for API testing, documentation, and validation.

## 🚀 Features

- **Interactive API Documentation**: Auto-generated documentation with Swagger UI
- **Live API Testing**: Test endpoints directly from the browser interface
- **Request/Response Validation**: Automatic validation against OpenAPI schema
- **Multiple Environment Support**: Test against different API environments
- **Authentication Support**: Handle various authentication methods (Bearer, API Key, OAuth)
- **Export Capabilities**: Export API collections for Postman/Insomnia
- **Real-time Testing**: Live endpoint monitoring and testing
- **Response Formatting**: Beautiful JSON/XML response formatting

## 🛠 Tech Stack

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **API Documentation**: Swagger UI / OpenAPI 3.0
- **Testing Framework**: Swagger Codegen
- **Styling**: Bootstrap 5 / Material Design
- **HTTP Client**: Axios / Fetch API
- **Build Tools**: Webpack / Vite
- **Validation**: JSON Schema Validator

## 📋 Prerequisites

- Node.js 16.0 or higher
- npm or yarn package manager
- Modern web browser (Chrome, Firefox, Safari, Edge)

## 🔧 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/PrasetyoWibowoo/api-testing-swagger.git
   cd api-testing-swagger
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Configure API endpoints**
   ```bash
   # Copy environment template
   cp .env.example .env
   
   # Edit your API configurations
   nano .env
   ```

4. **Start development server**
   ```bash
   npm run dev
   # or
   yarn dev
   ```

5. **Open in browser**
   ```
   http://localhost:3000
   ```

## 🏗 Project Structure

```
api-testing-swagger/
├── src/
│   ├── components/           # Reusable UI components
│   │   ├── ApiTester/       # API testing interface
│   │   ├── SwaggerUI/       # Swagger UI integration
│   │   └── ResponseViewer/  # Response display component
│   ├── config/              # Configuration files
│   │   ├── swagger.config.js
│   │   └── api.config.js
│   ├── utils/               # Utility functions
│   │   ├── apiClient.js     # HTTP client wrapper
│   │   ├── validator.js     # Request/response validation
│   │   └── formatter.js     # Response formatting
│   ├── styles/              # CSS/SCSS files
│   │   ├── main.css
│   │   └── components/
│   ├── assets/              # Static assets
│   │   ├── images/
│   │   └── icons/
│   └── index.html           # Main HTML file
├── public/                  # Public assets
├── docs/                    # API documentation
│   └── openapi.yaml         # OpenAPI specification
├── tests/                   # Test files
├── .env.example             # Environment variables template
├── package.json
└── README.md
```

## 📖 API Documentation

### OpenAPI Specification

The project uses OpenAPI 3.0 specification for API documentation. The main specification file is located at `docs/openapi.yaml`.

```yaml
openapi: 3.0.0
info:
  title: API Testing Demo
  description: Sample API for testing purposes
  version: 1.0.0
servers:
  - url: https://api.example.com/v1
    description: Production server
  - url: https://staging-api.example.com/v1
    description: Staging server
```

### Supported Authentication Methods

- **Bearer Token**
  ```javascript
  headers: {
    'Authorization': 'Bearer your-jwt-token'
  }
  ```

- **API Key**
  ```javascript
  headers: {
    'X-API-Key': 'your-api-key'
  }
  ```

- **Basic Authentication**
  ```javascript
  headers: {
    'Authorization': 'Basic ' + btoa('username:password')
  }
  ```

## 🚦 Usage

### 1. Testing API Endpoints

```javascript
// Example: Testing a GET endpoint
const testGetEndpoint = async () => {
  try {
    const response = await apiClient.get('/users', {
      headers: {
        'Authorization': 'Bearer your-token'
      }
    });
    
    console.log('Response:', response.data);
    validateResponse(response.data, userSchema);
  } catch (error) {
    console.error('API Error:', error);
  }
};
```

### 2. Adding New API Endpoints

1. Update the OpenAPI specification in `docs/openapi.yaml`
2. Add endpoint configuration in `src/config/api.config.js`
3. Refresh the Swagger UI to see new endpoints

### 3. Environment Configuration

```javascript
// src/config/api.config.js
export const environments = {
  development: {
    baseURL: 'http://localhost:8080/api',
    timeout: 5000
  },
  staging: {
    baseURL: 'https://staging-api.example.com/v1',
    timeout: 10000
  },
  production: {
    baseURL: 'https://api.example.com/v1',
    timeout: 15000
  }
};
```

## 🔍 Features in Detail

### Interactive API Testing
- Send HTTP requests directly from the browser
- Support for all HTTP methods (GET, POST, PUT, DELETE, PATCH)
- Real-time request/response visualization
- Request history and bookmarking

### Response Validation
```javascript
// Automatic response validation
const validateApiResponse = (response, schema) => {
  const validator = new JSONSchemaValidator();
  const isValid = validator.validate(response, schema);
  
  if (!isValid) {
    console.warn('Response validation failed:', validator.errors);
  }
  
  return isValid;
};
```

### Export Collections
Export your tested endpoints to popular API clients:
- Postman Collection (JSON)
- Insomnia Workspace
- cURL commands

## 🧪 Testing

Run the test suite:

```bash
# Unit tests
npm run test

# Integration tests
npm run test:integration

# E2E tests
npm run test:e2e

# Coverage report
npm run test:coverage
```

## 📦 Build & Deployment

### Development Build
```bash
npm run build:dev
```

### Production Build
```bash
npm run build:prod
```

### Deploy to GitHub Pages
```bash
npm run deploy
```

### Docker Deployment
```bash
# Build Docker image
docker build -t api-testing-swagger .

# Run container
docker run -p 3000:3000 api-testing-swagger
```

## 🔧 Configuration

### Environment Variables

```bash
# .env file
VITE_API_BASE_URL=https://api.example.com/v1
VITE_SWAGGER_URL=/docs/openapi.yaml
VITE_ENABLE_CORS=true
VITE_DEFAULT_TIMEOUT=10000
```

### Swagger Configuration

```javascript
// src/config/swagger.config.js
export const swaggerConfig = {
  url: process.env.VITE_SWAGGER_URL,
  dom_id: '#swagger-ui',
  deepLinking: true,
  presets
