# Task Scheduler - Multi-Threaded Web Application

A simple multi-threaded task scheduling tool web application built with Java and HTML. This application allows you to schedule, manage, and monitor tasks with a beautiful, modern web interface.

## Features

- 🚀 **Multi-threaded task scheduling** - Handles multiple tasks concurrently
- 📋 **Task management** - Schedule, cancel, and view tasks
- 🎨 **Modern UI** - Bright, colorful interface with smooth transitions and animations
- ⚡ **Real-time updates** - Automatic task status refresh every 2 seconds
- 🐳 **Docker support** - Easy deployment with Docker and Docker Compose
- 🔄 **Task status tracking** - Monitor tasks through their lifecycle (SCHEDULED → RUNNING → COMPLETED/CANCELLED)

## Requirements

- Docker and Docker Compose
- OR Java 17+ (if running without Docker)

## Quick Start

### Using Docker (Recommended)

1. **Build and start the application:**
   ```bash
   docker-compose up -d --build
   ```

2. **Access the application:**
   - Open your browser and navigate to: `http://localhost:8092`

3. **View logs:**
   ```bash
   docker-compose logs -f
   ```

4. **Stop the application:**
   ```bash
   docker-compose down
   ```

### Running without Docker

1. **Compile the Java application:**
   ```bash
   javac -d classes -sourcepath src/main/java src/main/java/com/taskscheduler/TaskScheduler.java
   ```

2. **Run the application:**
   ```bash
   java -cp classes com.taskscheduler.TaskScheduler
   ```

3. **Access the application:**
   - Open your browser and navigate to: `http://localhost:8080`

## Configuration

### Port Configuration

The default port is **8092** (configured in `docker-compose.yml`). To change the port:

1. Edit `docker-compose.yml`:
   ```yaml
   ports:
     - "YOUR_PORT:8080"
   ```

2. Restart the container:
   ```bash
   docker-compose down
   docker-compose up -d
   ```

## Usage

### Scheduling a Task

1. Enter a task name in the "Task Name" field
2. Select a task type (Simple, Complex, or Priority)
3. Set the delay in seconds (1-60)
4. Click "Schedule Task"

### Viewing Tasks

- All scheduled tasks are displayed automatically
- Tasks refresh every 2 seconds
- Click "Refresh" to manually update the task list

### Cancelling a Task

- Click the "Cancel" button on any scheduled or running task
- Cancelled tasks cannot be resumed

## Task Statuses

- **SCHEDULED** - Task is scheduled but not yet running
- **RUNNING** - Task is currently executing
- **COMPLETED** - Task has finished successfully
- **CANCELLED** - Task was cancelled before completion

## API Endpoints

The application provides the following REST API endpoints:

### Schedule a Task
- **Endpoint:** `POST /api/schedule`
- **Parameters:**
  - `name` - Task name (required)
  - `type` - Task type: simple, complex, or priority (optional, default: simple)
  - `delay` - Delay in seconds (optional, default: 5)
- **Example:**
  ```bash
  curl -X POST http://localhost:8092/api/schedule \
    -d "name=My Task&type=simple&delay=10"
  ```

### Cancel a Task
- **Endpoint:** `POST /api/cancel`
- **Parameters:**
  - `taskId` - Task ID to cancel (required)
- **Example:**
  ```bash
  curl -X POST http://localhost:8092/api/cancel \
    -d "taskId=task-1"
  ```

### Get All Tasks
- **Endpoint:** `GET /api/tasks`
- **Returns:** JSON array of all tasks
- **Example:**
  ```bash
  curl http://localhost:8092/api/tasks
  ```

### Health Check
- **Endpoint:** `GET /api/health`
- **Returns:** `{"status":"healthy"}`
- **Example:**
  ```bash
  curl http://localhost:8092/api/health
  ```

## Project Structure

```
Task sheduler/
├── src/
│   └── main/
│       └── java/
│           └── com/
│               └── taskscheduler/
│                   └── TaskScheduler.java
├── web/
│   └── index.html
├── Dockerfile
├── docker-compose.yml
└── README.md
```

## Technical Details

- **Backend:** Java 17 with built-in HTTP server
- **Frontend:** HTML5 with embedded CSS and JavaScript
- **Threading:** Uses `ExecutorService` with 10 threads for concurrent task execution
- **Task Execution:** Tasks run with a 2-second execution time simulation
- **Container:** Eclipse Temurin JDK 17

## Troubleshooting

### Port Already in Use

If port 8092 is already in use:

1. Change the port in `docker-compose.yml`
2. Or stop the service using the port:
   ```bash
   docker-compose down
   ```

### Container Won't Start

1. Check Docker is running:
   ```bash
   docker ps
   ```

2. View container logs:
   ```bash
   docker-compose logs
   ```

3. Rebuild the container:
   ```bash
   docker-compose down
   docker-compose build --no-cache
   docker-compose up -d
   ```

### Application Not Accessible

1. Verify the container is running:
   ```bash
   docker ps
   ```

2. Check if the port is correctly mapped:
   ```bash
   docker-compose ps
   ```

3. Test the health endpoint:
   ```bash
   curl http://localhost:8092/api/health
   ```

## License

This project is open source and available for personal and educational use.

## Author

Created by DILLIHARINI S 

