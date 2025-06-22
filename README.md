# Process Reclaim LMK (Inject)
![1000008074](https://github.com/user-attachments/assets/3c26a3bd-39dd-4779-ab1c-5d0cd89a92e3)

### A form of low memory killer daemon that prefers reclaim over immediate release
A custom low memory killer code injector for LMKD devices that specializes in reclaiming memory and prioritizes killing as few as possible, based on the project [prlmk](https://github.com/darkhz/prlmk/tree/README). Suitable mainly for devices with 4 GB of RAM or less, but devices with more memory can also benefit, even if only slightly.

The way it works is that it uses the Per-Process Reclaim driver to reclaim memory, having two thresholds: swap free and free file limit. If the swap free reaches a critical limit, processes with lower CPU usage are killed (using stime+utime for this) to satisfy the memory demands, continuing to kill these processes until the swap free threshold is met and is higher. If it exceeds the free file limit, the process that consumes the most memory with adj score of 701> is killed to satisfy the extreme usage.

### Requirements
- Have at least 1 GB of ZRAM or Swapfile, or both. Larger than 1GB is preferred.
- Have LMKD, please do not use this module if you have LMK or Simple LMK, it is only compatible with LMKD.
- Errors may occur in certain versions of Android, after all, this module that I created I am only testing on Android 15 in the Lineage OS ROM, so older and later versions need testing.
- It can only be used for devices that have PPR (Per-Process Reclaim) commonly found in Snapdragon devices, maybe it can be found in others, it is not known.
