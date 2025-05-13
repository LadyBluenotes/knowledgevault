- npm provides various features to help install and maintain project depedencies
- dependencies get updates with new features and fixes so upgrading to a newer version is recommend

1. **Install npm Check Updates**

```bash
npm install -g npm-check-updates
```

2. Run npm Check Updates

- Cd to a directory with your project and run the following command `npm ncu` which will return a list of packages that need to be updated
- The existing version is on the left and the latest is on the right
  - NPU maintains semantic versioning policies so you can quickly identify packages, minor updates, or major updates that need fixing

2. **Update patches**

- Update packages, assuming the package maintainers are following semantic versioning it shouldnt break anything
- Following up with `npm i` will ensure everything is still working and commit the changes (so it can be reverted, if necessary)

```bash
npx ncu -u -t patch

npm i
```

4. **Update minor versions**

- Update minor version updates next - this should also not break anything if following semantic versioning
- Similar to patches, run `npm i` and commit the changes

```bash
npx ncu -u -t minor

npm i
```

5. **Update major versions**

- Before updating these, read release not docs to see how the new version will affect your project
- Once you know, update each major change in a separate commit
- NCU lets you filter for a specific package by using `--filter` or `-f` flag

```bash
npx ncu -u -f <package-name>

npm i
```
