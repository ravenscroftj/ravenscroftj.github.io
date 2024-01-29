-
- ## Filament Nexus issue
- ```
  10.43 npm WARN deprecated @hapi/joi@15.1.1: Switch to 'npm install joi'
  12.86 npm notice 
  12.86 npm notice New patch version of npm available! 10.2.3 -> 10.2.5
  12.86 npm notice Changelog: <https://github.com/npm/cli/releases/tag/v10.2.5>
  12.86 npm notice Run `npm install -g npm@10.2.5` to update!
  12.86 npm notice 
  12.87 npm ERR! code E401
  12.87 npm ERR! Unable to authenticate, need: BASIC realm="Sonatype Nexus Repository Manager"
  12.88 
  12.88 npm ERR! A complete log of this run can be found in: /root/.npm/_logs/2023-12-11T11_50_35_801Z-debug-0.log
  -----
  ```
- Can happen when someone has nexus set up as their npm repo
- Best thing to do is find/replace in package lock:
	- Find: `https://nexus.filament.ai/repository/npm/`
	- Replace: `https://registry.npmjs.org/`