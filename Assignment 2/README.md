### BUFFER POOL FUNCTIONS

# initBufferPool:
- Creates a new buffer pool in memory.  
- `pageFileName` stores the name of the page file whose pages are cached.  
- `numPages` defines the buffer size (number of page frames).  
- `strategy` specifies the replacement strategy (FIFO, LRU).  
- `stratData` is not used here.  

# shutdownBufferPool:
- Destroys the buffer pool and frees memory.  
- Flushes unpinned dirty pages before closing.  
- Shutdown still succeeds even if some pages remain pinned.  

# forceFlushPool
- Writes all dirty pages with `fixCount = 0` to disk.  

---

### PAGE MANAGEMENT FUNCTIONS

# pinPage:
- Loads the requested page into the buffer.  
- If full, a replacement strategy (FIFO or LRU) chooses a victim.  
- If the victim is dirty, it is written back before replacement.  

# unpinPage:
- Decrements the `fixCount` of a page by 1.  

# markDirty:
- Sets the `dirty` flag of a page to `TRUE`.  

# forcePage:
- Writes the page back to disk if it is dirty.  

---

### STATISTICS FUNCTIONS

# getFrameContents:
- Returns an array of page numbers in the buffer.  

# getDirtyFlags:
- Returns an array of dirty flags for each frame.  

# getFixCounts:
- Returns an array of fix counts for each frame.  

# getNumReadIO:
- Returns the total number of pages read from disk.  

# getNumWriteIO:
- Returns the total number of pages written to disk.  

---

### PAGE REPLACEMENT ALGORITHM FUNCTIONS

The implemented strategies are **FIFO** and **LRU**.  

# FIFO:
- Replaces the page that entered the buffer earliest.  

# LRU:
- Replaces the page that was least recently used.  
