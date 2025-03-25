# Create Database Script

This repository contains scripts to create an SQLite database in various programming languages including Bash, PowerShell, and C.

## Bash Script

### Description
The Bash script checks if a database file exists, creates the database if it doesn't, and prints a success message. If the database already exists, it informs the user.

### Script

```bash
#!/bin/bash

# Function to create a database
create_database() {
    local db_name="$1"
    if [ -f "$db_name" ]; then
        echo "Database '$db_name' already exists."
    else
        sqlite3 "$db_name" ".databases" >/dev/null 2>&1
        if [ $? -eq 0 ]; then
            echo "Database '$db_name' created successfully."
        else
            echo "Error accessing database."
        fi
    fi
}

# Check if an argument is provided, use it as the database name
# If no argument is provided, default to "mydatabase.db"
if [ $# -gt 0 ]; then
    create_database "$1"
else
    create_database "mydatabase.db"
fi
