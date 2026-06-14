## Day 1 — June 14, 2026
- Set up repo and folder structure
- Wrote initial docker-compose.yml
- Hit issue: Wazuh indexer kept crashing → fixed by increasing vm.max_map_count
- Dashboard accessible at https://localhost

## Day 2
- Added alpine-target container
- Installed Wazuh agent inside it
- First log appeared in dashboard 🎉