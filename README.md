# PES manifest

```bash
├── generate_manifest.py # Script which creates manifest from three files with packages
├── pes_backend_packages.txt # Python packages used in PES
├── pes_container_packages.txt # System packages present in prod container
├── pes_frontend_packages.txt # Packages used by react on FE
├── pes_manifest.txt # contains manifest for Packge Evolution Service
└── README.md
```

## How to refresh manifest

1. Refresh pes_container_packages.txt
    - Go to production pod in openshift and run `rpm -qa`
    - Note: When refreshing container packages, remove kernel entry if needed.
2. Refresh pes_backend_packages.txt
    - Go to production pod in openshift and run `pip freeze`
3. Refresh pes_frontend_packages.txt
    - Run `npm list | cut -d " " -f2 | replace @ -` in FE repository
4. Check `Dockerfile` in `pes-housekeeping` repo (`mpp` branch) on private GitLab and if needed change image name in `generate_manifest.py`
5. Run `generate_manifest.py`
6. Create PR with changes
