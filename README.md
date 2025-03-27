# AI Code Review Tool

## Overview
The AI Code Review Tool is a microservices-based system built using **ASP.NET Core**. It integrates AI-powered code review capabilities, authentication, GitHub and Visual Studio integration, file processing, logging, and monitoring.

## Architecture
The system follows a **microservices architecture** and consists of the following components:

### Microservices & Technologies Used
| Project Name                 | Microservice Name               | Project Type                                     |
|------------------------------|---------------------------------|-------------------------------------------------|
| **APIGateway**              | API Gateway                     | ASP.NET Core Web API (**Ocelot**)               |
| **CodeReviewService**       | Code Review Service             | ASP.NET Core Web API (**Ollama**)               |
| **FileProcessingService**   | File Processing Service         | ASP.NET Core Web API (**RabbitMQ**)            |
| **GitHubIntegrationService** | GitHub & VS Integration Service | ASP.NET Core Web API (**GitHub API**)          |
| **AuthService**             | Authentication Service          | ASP.NET Core Identity (**OAuth2.0**)           |
| **LoggingService**          | Logging & Monitoring Service    | ASP.NET Core Web API (**Serilog, Prometheus**) |

## AI Code Review - Best Open-Source Models
For AI-powered **code review**, the following **open-source** models can be used with **Ollama**:

| **Model**            | **Description** | **Languages Supported** |
|----------------------|----------------|------------------------|
| **CodeLlama**        | Meta’s model fine-tuned for code generation and understanding | Python, C#, Java, JavaScript, C++, Go, etc. |
| **StarCoder**        | Open-weight model trained on 80+ programming languages | Python, JavaScript, Java, TypeScript, C++, C# |
| **WizardCoder**      | Fine-tuned for code generation and refactoring | Python, C++, Java, JavaScript |
| **Phind-CodeLlama**  | Optimized for developer Q&A, code explanations, and debugging | Python, C++, JavaScript, Java |

### **Best Model Selection Based on Use Case**
- **General Code Review & Bug Detection** → **StarCoder**  
- **AI-Powered Code Suggestions & Completion** → **WizardCoder**  
- **Code Understanding & Explanations** → **CodeLlama**  
- **Developer Q&A & Debugging** → **Phind-CodeLlama**  

## Development Roadmap

### 1. Web-Based Code Review
- [ ] Setup ASP.NET Core Backend
- [ ] Implement API for text input
- [ ] Implement API for multiple file uploads
- [ ] Integrate Ollama for AI Code Review

### 2. Visual Studio Extension
- [ ] Create VSIX Project in Visual Studio
- [ ] Add a custom command to send code for review
- [ ] Call API from VSIX to send the active document
- [ ] Display AI feedback in Visual Studio

### 3. GitHub Integration
- [ ] Set up GitHub Webhooks to trigger reviews
- [ ] Use GitHub API to fetch code from repositories
- [ ] Post AI feedback as PR comments
- [ ] Automate reviews in GitHub Actions

## Architecture Diagram
The following diagram illustrates how the AI Code Review Tool integrates with **Web UI, Visual Studio Extension, and GitHub**:

```mermaid
graph TD;
    User -->|Submits Code| WebUI;
    WebUI -->|Sends Code| APIGateway;
    APIGateway -->|Routes Request| CodeReviewService;
    CodeReviewService -->|Processes with AI| Ollama;
    CodeReviewService -->|Stores Data| FileProcessingService;
    FileProcessingService -->|Uses| RabbitMQ;
    APIGateway -->|Routes to| AuthService;
    AuthService -->|Handles Authentication| OAuth2.0;
    APIGateway -->|Routes Logs| LoggingService;
    LoggingService -->|Monitors| Prometheus & Serilog;
    VSIX -->|Sends Code| APIGateway;
    APIGateway -->|Routes to| CodeReviewService;
    GitHub -->|Triggers Webhooks| GitHubIntegrationService;
    GitHubIntegrationService -->|Fetches Code| GitHub API;
    GitHubIntegrationService -->|Posts AI Feedback| PullRequestComments;
```

## Installation & Setup
### Prerequisites
Ensure you have the following installed:
- **.NET 8 SDK**
- **Docker** (for containerization)
- **RabbitMQ** (for message queuing)
- **Prometheus & Grafana** (for monitoring)
- **Ocelot** (for API Gateway)

### Clone the Repository
```sh
git clone https://github.com/your-repo/ai-code-review-tool.git
cd ai-code-review-tool
```

### Build and Run Services
Each microservice is self-contained and can be run separately. You can start all services using Docker Compose:
```sh
docker-compose up --build
```

Alternatively, run individual services manually:
```sh
dotnet run --project APIGateway
```

## API Endpoints
### API Gateway (Ocelot)
- `GET /api/review` - Get code review results
- `POST /api/review` - Submit code for review

### Authentication Service
- `POST /api/auth/login` - User login
- `POST /api/auth/register` - User registration

### File Processing Service
- `POST /api/files/upload` - Upload a file for processing

### GitHub Integration Service
- `GET /api/github/repos` - Get user repositories

### Logging Service
- `GET /api/logs` - Retrieve application logs

## Contributing
1. Fork the repository
2. Create a feature branch (`git checkout -b feature-name`)
3. Commit changes (`git commit -m 'Add new feature'`)
4. Push to the branch (`git push origin feature-name`)
5. Create a Pull Request

## License
This project is licensed under the MIT License.

## Contact
For questions or support, contact **your-email@example.com** or open an issue on GitHub.

