# Network Top Processes 

## Overview

This Python script provides a comprehensive analysis of your computer's top network connections. By utilizing the `psutil` library, it gathers information about established network connections (both IPv4 and IPv6) and presents it in a user-friendly manner. The script aims to help you understand your network's performance, resource usage, and potential security risks.

## Prerequisites

Before running the script, ensure you have the following requirements:

1. Python 3.x installed on your system.
2. The `psutil` library installed. You can install it using pip: `pip install psutil`.
3. The `matplotlib` and `tabulate` libraries also installed. If you don't have them, install them using pip: `pip install matplotlib tabulate`.
4. Run as sudo. 

## Usage

1. Save the script to a file named `network_connections_analyzer.py`.
2. Open your terminal or command prompt.
3. Navigate to the directory where the script is saved.
4. Run the script by typing: `python network_connections_analyzer.py`.

## Functionality

Upon execution, the script performs the following tasks:

1. Retrieves a list of all network connections (both IPv4 and IPv6) using `psutil.net_connections`.
2. Counts the number of connections per process, considering only established connections.
3. Displays a tabular summary of the top 10 processes with the most connections, ordered by connection count.
4. Provides detailed information about each network connection of the top processes, including PID, local address, remote address, and status.
5. Creates a bar chart illustrating the top processes and their connection counts using `matplotlib`.

