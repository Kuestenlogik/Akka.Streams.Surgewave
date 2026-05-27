# Maintainer Guide

Internal documentation for Akka.Streams.Surgewave maintainers.

## Release Process

### 1. Prepare
```bash
# Ensure main is clean and all tests pass
dotnet test Akka.Streams.Surgewave.slnx -c Release -v normal

# Verify version bumps in Directory.Build.props if needed
```

### 2. Tag and Push
```bash
# Stable release
git tag v0.1.0
git push --tags

# Pre-release
git tag v0.2.0-rc.1
git push --tags
```

### 3. What Happens Automatically
- `.github/workflows/release.yml` triggers on `v*` tag push
- Build + Test + Pack run against the tag version
- `*.nupkg` → GitHub Packages (stable + pre-release)
- `*.nupkg` → nuget.org (stable only, gated on `NUGET_API_KEY` secret)
- GitHub Release with auto-generated notes + attached nupkg files

## Tag Naming

- `v{major}.{minor}.{patch}` — stable
- `v{major}.{minor}.{patch}-rc.{n}` — release candidate (skipped on nuget.org push)

## Secret requirements

| Secret | Scope | Used for |
|---|---|---|
| `NUGET_API_KEY` | Org-level | nuget.org publish (gate on `env.X != ''`). Glob must include `Kuestenlogik.Akka.Streams.Surgewave*` — the package ships under the `Kuestenlogik.*` namespace because the `Akka.*` prefix on nuget.org is verified-reserved by the Akka.NET team. |
| `KUESTENLOGIK_PACKAGES_TOKEN` | Org-level | Restore from GitHub Packages during build (Surgewave-Client dependency) |

If `NUGET_API_KEY` is missing, the workflow skips nuget.org silently and
GitHub Packages still receives the build.

## NuGet package naming

| Property | Value |
|---|---|
| **PackageId** | `Kuestenlogik.Akka.Streams.Surgewave` |
| **Namespace** | `Akka.Streams.Surgewave` (unchanged — follows Akka.Streams convention) |
| **Assembly name** | `Akka.Streams.Surgewave` (unchanged) |
| **Repo / csproj** | `Akka.Streams.Surgewave` (unchanged) |

The PackageId-only rewrite happens in `Directory.Build.props`:
`<PackageId>Kuestenlogik.$(MSBuildProjectName)</PackageId>`. xunit-Pattern:
PackageId `xunit.v3` ships namespace `Xunit`.
