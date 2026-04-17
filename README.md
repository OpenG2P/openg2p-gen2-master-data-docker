# openg2p-gen2-master-data-docker

Docker creation files and scripts for the OpenG2P Gen2 Master Data API.

- scripts/build.sh: local CLI equivalent of the GitHub Actions docker build workflow
- test/local_build.py: lightweight local build helper for a single service spec
- Service specs live under openg2p-gen2-master-data and drive image name plus dependency versions
- GitHub Actions requires a version like 1.0, v1.0.0, v1.0.1, or develop and builds the master data API spec for that version
