---
name: evaluate-dependency
description: Before adding or upgrading a third-party dependency, weigh the need against stdlib, then check maintenance health, security, license, size, and the lighter alternative. Use when considering a new library or a version bump, or asked whether to add or replace a dependency.
---

Every dependency is a liability you take on forever — its bugs, its breakage, its maintenance, its supply-chain risk. Adopt one only when it removes more complexity than it adds. Apply the same alternatives discipline as design (`../../references/design-principles.md`).

## Steps

1. **Justify the need.** What does this remove that the standard library or a few lines of your own wouldn't? A dependency you'd use once, or could write in five readable lines, isn't worth the liability — stop here and write it.
2. **Check the health.** Maintenance (recent releases, open-vs-closed issue ratio, bus factor), adoption (is it the de-facto choice in this ecosystem), and documentation. An unmaintained library is a migration you've scheduled for your future self.
3. **Check the risk.** Known CVEs, the transitive dependencies it drags in, the license (compatible with yours?), and the install/bundle size it adds.
4. **Name the alternatives.** The stdlib path, a lighter library, and the write-it-yourself option — each with its real cost, laid out as contenders (not a strawman beside the one you already picked). Recommend one, tied to this project's constraints.
5. **For an upgrade**, read the changelog for breaking changes and estimate the migration cost before bumping. Pin the version either way.

## Completion

The need is justified against stdlib and DIY; the library's maintenance, security, license, and size are checked; the lighter alternatives are named with their tradeoffs and one is recommended for this project; the version is pinned, and for an upgrade the breaking changes were read.
