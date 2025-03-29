# Driver Monitoring System

This system helps monitor and analyze system drivers, allowing you to identify suspicious or new drivers using the `driverquery -v` command.

## Features

- View current system drivers with detailed information
- Save snapshots of drivers for baseline comparison
- Compare current drivers with previous snapshots to identify changes
- Flag potentially suspicious drivers based on predefined patterns
- Filter and search through driver information
- Detailed view of individual driver properties

## Components

1. **Server**: Node.js Express server that interacts with the system's `driverquery` command
2. **Client**: Web-based dashboard to visualize and interact with driver data

## Prerequisites

- Node.js (v14+) installed
- Windows operating system (for `driverquery` command support)
- Administrative privileges (to run `driverquery -v`)

## Installation

1. Create a new directory for the project:
   ```
   mkdir driver-monitoring
   cd driver-monitoring
   ```

2. Create two files:
   - `server.js` - Copy the server code
   - `index.html` - Copy the client code

3. Initialize a new Node.js project and install dependencies:
   ```
   npm init -y
   npm install express cors child_process
   ```

## Running the Application

1. Start the server:
   ```
   node server.js
   ```

2. Open the client:
   - Simply open the `index.html` file in a web browser
   - Or serve it using a simple HTTP server

## Usage Guide

### Initial Setup

1. Start the server with administrative privileges
2. Open the client in your browser
3. Click "Load Current Drivers" to see the current state of drivers on your system
4. Click "Save Snapshot" to create a baseline for future comparisons

### Regular Monitoring

1. Click "Load Current Drivers" to refresh the current state
2. Click "Compare With Baseline" to see what has changed since your last snapshot
3. Use the filters to focus on suspicious, new, or modified drivers
4. Search for specific drivers using the search box
5. Click on any driver row to view detailed information

### Understanding the Dashboard

- **New Drivers**: Highlighted in green, these are drivers that weren't in the previous snapshot
- **Modified Drivers**: Highlighted in blue, these are drivers with changed properties
- **Suspicious Drivers**: Highlighted in yellow, these match patterns that might indicate unusual behavior
- **Removed Drivers**: Not shown in the main table, but counted in the comparison statistics

### Suspicious Patterns

The system flags drivers as suspicious based on these patterns:

- Binary located in temporary directory
- Binary located in downloads folder
- Random-looking module names
- Auto-starting drivers
- Empty descriptions
- Unusually short display names

## Customization

### Modifying Suspicious Patterns

Edit the `suspiciousPatterns` array in the client code to add or modify patterns:

```javascript
const suspiciousPatterns = [
  { field: 'binaryPathName', pattern: /your-pattern/i, reason: 'Your reason' },
  // Add more patterns
];
```

### Adding More Analysis

The server can be extended to perform additional analysis on drivers. Consider adding:

- Digital signature verification
- File hash comparison
- Known-good/known-bad lists
- Timeline visualization of driver changes

## Security Considerations

- This tool requires administrative privileges to run `driverquery -v`
- The server only allows local connections by default
- No authentication is implemented - add this if used in a shared environment
- The tool helps identify suspicious patterns but is not a replacement for a full security solution

## Troubleshooting

- **Permission errors**: Ensure the server is running with administrative privileges
- **Empty driver list**:

  
