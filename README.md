# MediCare Management API

A clinic management system Web API built with **ASP.NET Core 8.0**, **Entity Framework Core**, and **SQL Server**. It exposes role-based endpoints for the day-to-day operations of a small hospital / clinic — appointments, prescriptions, billing, lab tests, pharmacy inventory, and user management — secured with JWT bearer authentication.

## Tech Stack

- ASP.NET Core 8.0 Web API
- Entity Framework Core 7.0 (SQL Server)
- JWT Bearer Authentication
- Swagger / Swashbuckle (OpenAPI)
- Repository + Service layered architecture

## Roles

The API supports the following roles, each with its own controller:

- **Admin** — manages doctors, departments, and overall system data
- **Receptionist** — patient registration, appointment scheduling, consultation billing
- **Doctor** — patient history, prescriptions, lab test orders
- **Pharmacist** — medicine inventory, dispensing, pharmacy bills
- **Lab Technician** — lab inventory, test results, lab bills

## Project Structure

```
MediCareCMSWebApi-Solution/
├── MediCareCMSWebApi.sln
└── MediCareCMSWebApi/
    ├── Controllers/      # AdminController, DoctorController, ReceptionistController,
    │                     # PharmacistControllers, LabTechnicianControllers, LoginsController
    ├── Models/           # EF Core entities + MediCareDbContext
    ├── Repository/       # Data-access interfaces and implementations
    ├── Service/          # Business-logic interfaces and implementations
    ├── ViewModel/        # DTOs / view models for requests and responses
    ├── Program.cs        # DI, JWT, CORS, Swagger configuration
    └── appsettings.json  # Connection string + JWT settings
```

## Getting Started

### Prerequisites

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download)
- SQL Server (LocalDB, Express, or full instance)
- Visual Studio 2022 / VS Code / Rider

### Configuration

Update `MediCareCMSWebApi/appsettings.json` with your own values:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=YOUR_SERVER;Database=MediCareDb;Trusted_Connection=True;TrustServerCertificate=True;"
  },
  "Jwt": {
    "Key": "YOUR_SECRET_KEY_AT_LEAST_32_CHARS",
    "Issuer": "MediCareApi"
  }
}
```

### Run

```bash
cd MediCareCMSWebApi
dotnet restore
dotnet ef database update
dotnet run
```

The API starts on the URL printed in the console (typically `https://localhost:7xxx`). Swagger UI is available at `/swagger` in development.

## Authentication

1. `POST /api/Logins/login` with valid credentials returns a JWT.
2. Send subsequent requests with `Authorization: Bearer <token>`.
3. In Swagger UI, paste the token (without the `Bearer ` prefix) in the **Authorize** dialog.

## CORS

The default policy `AllowAllOrigin` allows the Angular front-end at `http://localhost:4200`. Adjust `Program.cs` if your client runs elsewhere.

## License

This project is provided as-is for educational / internal use.
