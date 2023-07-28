sudimport psutil
import matplotlib.pyplot as plt
from tabulate import tabulate

def get_top_processes_with_connections_info():
    # Get a list of all network connections (IPv4 and IPv6)
    connections = psutil.net_connections(kind='inet') + psutil.net_connections(kind='inet6')

    # Dictionary to store process names and their connection count
    process_connections = {}

    # Iterate through all connections and count the number of connections per process
    for conn in connections:
        if conn.status == psutil.CONN_ESTABLISHED:
            pid = conn.pid
            process_name = psutil.Process(pid).name()
            process_connections[process_name] = process_connections.get(process_name, 0) + 1

    # Sort the processes by the number of connections in descending order
    sorted_processes = sorted(process_connections.items(), key=lambda x: x[1], reverse=True)

    # Display the top processes and their connection counts in a table
    table_data = [(process, connection_count) for process, connection_count in sorted_processes[:10]]
    print(tabulate(table_data, headers=["Process", "Connections"], tablefmt="grid"))

    # Get detailed information for each network connection of the top process
    for process, _ in sorted_processes[:10]:
        print(f"\nDetailed Connection Information for {process}:")
        print("  PID    LADDR                                   RADDR                             STATUS")
        detailed_info = []
        process = psutil.Process(pid)
        connections = process.connections(kind='inet')
        for conn in connections:
            if conn.status == psutil.CONN_ESTABLISHED:
                detailed_info.append([pid, f"{conn.laddr.ip}:{conn.laddr.port}", f"{conn.raddr.ip}:{conn.raddr.port}", conn.status])
        print(tabulate(detailed_info, tablefmt="grid"))

    # Create a bar chart for the top processes and their connection counts
    top_processes = [process for process, _ in sorted_processes[:10]]
    connection_counts = [connection_count for _, connection_count in sorted_processes[:10]]
    
    plt.figure(figsize=(10, 6))
    plt.bar(top_processes, connection_counts, color='skyblue')
    plt.xlabel('Processes')
    plt.ylabel('Connection Count')
    plt.title('Top Processes by Connection Count')
    plt.xticks(rotation=45, ha='right')
    plt.tight_layout()
    plt.show()

if __name__ == "__main__":
    get_top_processes_with_connections_info()
