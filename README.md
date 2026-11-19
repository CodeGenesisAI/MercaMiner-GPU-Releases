# MercaMiner GPU — downloads

Solo OpenCL GPU miner for **Mercatura (MCA)**: MercaHash V1 and V2, NVIDIA and
AMD, Windows and Linux. This repository hosts the ready-to-run downloads and the
user manual. It does not contain source code.

## Download

Get the latest build from the [**Releases**](../../releases) page:

| Platform | File |
| --- | --- |
| Windows (64-bit) | `MercaMiner-GPU-vX.Y.Z-win64.zip` |
| Linux (64-bit) | `MercaMiner-GPU-vX.Y.Z-linux-x64.tar.gz` |

The Linux build is portable (glibc 2.17+, so Ubuntu 18.04 and newer and the
common mining OSes); the Windows build is a single static `.exe` with no extra
DLLs. Unzip or untar it and run.

## Features

- MercaHash **V1 and V2**, with an automatic switch at the fork height
- **Solo** mining straight to your own Mercatura Core node — every block pays the full reward to your wallet, no pool, no fee
- **SRBMiner-style** single command line, per-GPU settings, optional config file
- **NVIDIA + AMD**, multiple GPUs, automatic VRAM sizing
- NVIDIA core/memory clock, power and fan control; per-GPU **temperature pause** (NVIDIA, and AMD on Linux)
- **JSON statistics API** and SRBMiner-format console output — works with MatrixMinerOS / MatrixMinerUI and similar dashboards
- Safety built in: GPU self-test against the official vectors at every start, CPU re-check of every found block, automatic recovery
- Tools: `gpu-autotune`, `gpu-bench`, `gpu-stress`

## Quick start

1. Run a synced **Mercatura Core node** (v0.1.3 or newer) with RPC enabled.
2. Unpack the download for your platform.
3. List your GPUs:
   - Windows: `mercaminer-gpu.exe --list-devices`
   - Linux: `./mercaminer --list-devices`
4. Start mining (replace the address, node IP and RPC login with your own):

   ```
   ./mercaminer -a mercahash -o http://192.168.1.100:27775 \
     -u YOUR_ADDRESS.myrig -p RPCUSER:RPCPASSWORD \
     --gpu-max-temp 71 --api-enable
   ```

   On Windows use `mercaminer-gpu.exe` with the same options, or edit
   `start-mining.bat` (`start-mining-admin.bat` for clock control). On Linux,
   edit `start.sh`.

### MatrixMinerOS / MatrixMinerUI

Put the command line in the flight sheet's arguments field; the dashboard reads
the hashrate from the miner's SRBMiner-format output or its JSON API (port
21550). Set clocks **either** in the mining OS **or** with the miner's
`--gpu-cclock` / `--gpu-fan` options, not both.

The complete option reference, API fields and troubleshooting are in
[**MANUAL.txt**](MANUAL.txt).

## License

MIT; see [LICENSE](LICENSE). MercaMiner GPU is a fork of MercaMiner, the
reference CPU miner for Mercatura. Third-party notices are in
[`licenses/`](licenses).
