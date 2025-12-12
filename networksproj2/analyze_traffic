


import pyshark
import matplotlib.pyplot as plt

# =====================================
# Network Traffic Analysis Script
# =====================================
# Project Overview:
# We will analyze the data and create visualizations like graphs using Python
# and incorporate them into a website using Flask. 
# Our roadmap:
# 1. Capture real network traffic using Wireshark
# 2. Export the capture to a file (.pcapng)
# 3. Process and analyze this data in Python to extract patterns
#    - Identify top talkers and protocols
#    - Compute bandwidth usage over time
# 4. Visualize the results with graphs and prepare them for the Flask dashboard
# 5. Demonstrate the complete system in the video presentation
# =====================================

# Load your capture file
cap = pyshark.FileCapture('NetworkTraffic.pcapng')

total_packets = 0
protocol_counts = {}
src_counts = {}

# Go through each packet
for packet in cap:
    total_packets += 1

    # Count the protocol type
    proto = packet.highest_layer
    protocol_counts[proto] = protocol_counts.get(proto, 0) + 1

    # Count the source IP addresses
    if 'IP' in packet:
        src = packet.ip.src
        src_counts[src] = src_counts.get(src, 0) + 1

# Print results
print("Total packets:", total_packets)
print("\nProtocol counts:")
for proto, count in protocol_counts.items():
    print(f"{proto}: {count}")

print("\nTop source addresses:")
# Show top 10 talkers
top_src = sorted(src_counts.items(), key=lambda x: x[1], reverse=True)[:10]
for src, count in top_src:
    print(f"{src}: {count}")

# =====================================
# Visualization Section
# =====================================

# 1. Protocol Usage Bar Chart
plt.figure(figsize=(10,6))
plt.bar(protocol_counts.keys(), protocol_counts.values(), color='skyblue')
plt.title("Protocol Usage in Captured Traffic")
plt.xlabel("Protocol")
plt.ylabel("Number of Packets")
plt.xticks(rotation=45)
plt.tight_layout()
plt.savefig("protocol_usage.png")  # Save as PNG for Flask dashboard
plt.show()

# 2. Top Source IP Addresses Bar Chart
plt.figure(figsize=(10,6))
ips, counts = zip(*top_src)
plt.bar(ips, counts, color='orange')
plt.title("Top 10 Source IP Addresses")
plt.xlabel("Source IP")
plt.ylabel("Number of Packets")
plt.xticks(rotation=45)
plt.tight_layout()
plt.savefig("top_source_ips.png")  # Save as PNG for Flask dashboard
plt.show()

# 3. Optional: Pie Chart for Protocol Distribution
plt.figure(figsize=(8,8))
plt.pie(protocol_counts.values(), labels=protocol_counts.keys(), autopct='%1.1f%%', startangle=140)
plt.title("Protocol Distribution")
plt.tight_layout()
plt.savefig("protocol_distribution.png")
plt.show()

