# qBittorrent Analysis Project

*Team:* Dynamic Programmers  
- Anshuman Bhagat – 202301170 (G2)  
- Shashank Rawat – 202401183 (G3)  
- Shreyav Kumar – 202401206 (G3)

---

## Project Objective
This project provides a detailed analysis of *qBittorrent*, an open‑source, cross‑platform BitTorrent client. As part of our coursework, we have:
- Cloned and explored the qBittorrent codebase.  
- Investigated its architecture, data structures, and key modules.  
- Compiled implementation trade‑offs and design decisions.  

This README is designed for our project invigilator to easily understand our work, project structure, and findings, and to satisfy the academic evaluation criteria.

## Background
qBittorrent is a *peer‑to‑peer (P2P)* file sharing application based on the BitTorrent protocol. It enables decentralized downloading and uploading of files by splitting them into pieces and sharing across multiple peers.

## Key Features
- *Torrent Support:* Download from .torrent files or magnet links.  
- *Bandwidth Control:* Schedule/upload and download rate limits.  
- *Sequential Downloading:* Fetch pieces in order for previewing.  
- *IP Filtering:* Block peers by IP address or range.  
- *RSS Reader:* Automatic episode downloads via filter rules.  
- *Built‑in Search Engine:* (Optional) Plugins for popular torrent indexers.  
- *Web UI:* Remote control through a browser interface.  
- *Encryption:* Message Stream Encryption (MSE) and TLS support.  
- *Tracker & Peer Management:* Add/remove trackers; view peer stats.

## System Architecture
qBittorrent’s code is organized into several major modules:

1. *Core Module (C++ / libtorrent)*
   - Manages torrent sessions via [libtorrent] library.  
   - Handles piece distribution, hashing, and peer connections.  

2. *GUI Module (Qt / C++)*
   - Built with Qt for a responsive, cross‑platform interface.  
   - Integrates with core via well‑defined signal/slot mechanisms.

3. *Web UI (C++ backend + HTML/JS frontend)*
   - Exposes a RESTful API for remote torrent management.  
   - Designed for headless operation on servers or NAS devices.

4. *Search Engine Plugin System (Python)*
   - Extensible architecture allowing new indexer plugins.  
   - Parses HTML or JSON responses to present search results.

5. *Queue & Filter Manager*
   - Implements download priorities, category grouping, and queue logic.

## Data Structures
- *QMap / std::map*: Map torrent IDs to session and peer objects.  
- *QList / std::vector*: Store lists of active torrents, peers, and UI elements.  
- *QQueue*: FIFO queues for pending network packets and tasks.  
- **Custom Classes (e.g., TorrentInfo): Encapsulate metadata such as file lists, piece hashes, and tracker URLs.

## Design Approaches & Trade‑offs
- *Modularity:* Separation of GUI and core logic via libtorrent allows independent testing and maintenance.  
- *Asynchronous Programming:* Qt’s signal‑slot and libtorrent’s callbacks manage thousands of peers without blocking the UI.  
- *Container Choices:*
  - Qt containers integrate smoothly with Qt types (e.g., QVariant) but can incur slight overhead.  
  - STL containers (std::vector, std::map) are used in compute‑intensive paths for micro‑optimizations.  
- *Performance vs. Maintainability:*
  - Signal‑slot mechanisms improve readability at the cost of minor runtime overhead.  
  - Clear module interfaces add some complexity but greatly enhance code clarity and testability.
- *Memory vs. Speed:*
  - Balanced use of maps and simple arrays to minimize allocation overhead while providing fast lookups.

## Dependencies & Setup
1. *Qt* (version 5.x or 6.x)  
2. *libtorrent* (v1.2.x or later)  
3. *Python 3.x* (for search plugins)  
4. *C++17* or newer compiler  

bash
# Example build steps
git clone https://github.com/qbittorrent/qBittorrent.git
cd qBittorrent
mkdir build && cd build
cmake .. -DUSE_SYSTEM_LIBTORRENT=ON
make -j$(nproc)
sudo make install


## Usage
1. Launch the application (qbittorrent).  
2. Add a .torrent file or paste a magnet link.  
3. Monitor download progress in the main window.  
4. Access Web UI at http://localhost:8080 (default port).  

## Learning Outcomes
- Gained insight into a real‑world P2P application architecture.  
- Understood asynchronous network programming with Qt and libtorrent.  
- Analyzed container choices and performance trade‑offs in C++/Qt.  

---

Prepared by Dynamic Programmers for academic evaluation.
