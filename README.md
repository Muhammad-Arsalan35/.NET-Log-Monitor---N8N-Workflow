# .NET-Log-Monitor---N8N-Workflow
🚨 Automated .NET Application Error Detection & Analysis System
Overview
This n8n workflow automatically monitors .NET application log files, detects errors, provides AI-powered solutions, and sends detailed email reports to administrators.
Features
# Error Detection

Monitors daily log files automatically
Detects multiple error types: Database, .NET Framework, General
Extracts stack traces and error context
Identifies specific error patterns

# AI-Powered Solutions

Integrates with OpenRouter AI for intelligent error analysis
Provides actionable solutions for detected errors
Categorizes errors by type and severity

# Email Notifications

Sends formatted HTML email reports
Includes error details, stack traces, and solutions
Only sends emails when errors are found

# Database Logging

Stores all errors and solutions in database
Maintains historical error tracking
Enables trend analysis and reporting

# Prerequisites
Required Software

n8n (Self-hosted or Cloud)
Microsoft SQL Server (for database operations)
SMTP Server (for email notifications)

Required Credentials

Microsoft SQL Server Connection
OpenRouter AI API Key (for AI analysis)
SMTP Email Configuration

 # Installation
1. Import Workflow

Download dotnet-log-monitor.json
Open n8n
Go to Workflows → Import from file
Select the downloaded JSON file

2. Database Setup
Create the ErrorSolutions table in your SQL Server:
sqlCREATE TABLE ErrorSolutions (
    id INT IDENTITY(1,1) PRIMARY KEY,
    error_message NVARCHAR(MAX),
    stack_trace NVARCHAR(MAX),
    error_type VARCHAR(50),
    solution NVARCHAR(MAX),
    solution_type VARCHAR(50),
    timestamp DATETIME2,
    line_number INT,
    log_file_name VARCHAR(255),
    created_date DATETIME2 DEFAULT GETDATE()
);
3. Configure Credentials
Microsoft SQL Server

Go to Credentials → Create New
Select Microsoft SQL Server
Fill in your database connection details:

Host: your-sql-server
Database: your-database
Username: your-username
Password: your-password



OpenRouter AI API

Go to Credentials → Create New
Select HTTP Header Auth
Set:

Name: Authorization
Value: Bearer YOUR_API_KEY



Email (SMTP)

Go to Credentials → Create New
Select SMTP
Configure your SMTP settings

4. Customize Configuration
Update File Paths
Edit the "Read Log File" node:
javascript// Change this path to match your log file location
filePath: "C:/Logs/{{ $now.format('DDMMYYYY') }}_log.txt"
Update Email Settings
Edit the "Send Email Alert" node:
javascriptfromEmail: "noreply@yourcompany.com"  // Your sender email
toEmail: "admin@yourcompany.com"      // Recipient email
Schedule Configuration
Edit the "Cron Trigger" node:

Current: Every hour
Modify as needed (daily, every 30 minutes, etc.)
