# Network File System

This project implements a distributed file system that allows multiple clients to interact with storage servers through a naming server. It supports operations such as file creation, deletion, copying, reading, and writing, while ensuring synchronization and backup capabilities.

## Features Implemented

### Core Features
1. **File and Directory Operations**:
   - Create, delete, copy, read, and write files and directories.
   - Support for both synchronous and asynchronous writes.

2. **Backup Mechanism**:
   - Automatic backup of files to two additional storage servers for redundancy.
   - Backup paths are managed dynamically.

3. **Path Management**:
   - List all accessible paths from the root directory.
   - Trie-based structure for efficient path management.

4. **Client-Server Communication**:
   - Clients communicate with the naming server to locate storage servers.
   - Commands are sent using TCP sockets.

5. **Error Handling**:
   - Handles invalid paths, unavailable servers, and timeout scenarios.
   - Provides meaningful error messages to clients.

6. **Concurrency**:
   - Multi-threaded implementation for handling multiple client requests simultaneously.
   - Mutex locks and condition variables for synchronization.

7. **Caching**:
   - Caching mechanism for frequently accessed paths to improve performance.

8. **Health Monitoring**:
   - Periodic health checks for storage servers to ensure availability.

## Assumptions

1. **File/Directory Conflicts**:
   - The source file/directory being copied should not have name conflicts with existing destination files/directories.

2. **Accessible Paths**:
   - The `LIST_ALL_ACCESSIBLE_PATHS` function prints all paths from the assumed root directory.

3. **Write Format**:
   - `WRITE PATH DATA ASYN_FLAG`: If the flag is `1`, a forced synchronous write happens. If it is `0`, the storage server decides whether to write synchronously or asynchronously. The threshold for asynchronous writes is 1MB of data.

4. **Copy Operation**:
   - Works only when both source and destination are either directories or files.
   - Copy will not work if a client is writing to the file simultaneously.

5. **Unique Ports**:
   - All ports in the storage server for clients are unique.

6. **Streaming Files**:
   - Streaming files (e.g., music files) are not backed up.

7. **Server Identification**:
   - Each storage server is uniquely identified by its naming server port and client port.

8. **Backup Limitations**:
   - Backup does not work for write operations since acknowledgments are not sent to the naming server after a write.

9. **Timeouts**:
   - A timeout message is printed on the client side if no acknowledgment is received within 5 seconds, but the request is not terminated.
