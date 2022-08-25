# SLSA

*Supply chain Levels for Software Artifacts (SLSA, "salsa")* is a set of incremental supply chain security standards that consumers and producers of information artifacts can use to specify security guarantees for individual artifacts. SLSA levels 0-4 are targeted at the build component of the supply chain and describe increasingly tighter requirements for the safety of the build process. These levels are as follows:

* SLSA Level 0: No guarantees or security auditing whatsoever.
* SLSA Level 1: The build process is documented. Unsigned [provenance](provenance.md) is provided.
* SLSA Level 2: Requires hosted source/build system. Signed provenance. Prevents tampering after the build.
* SLSA Level 3: Requires certain security controls on host that houses source/build systems, veryfiable through auditing. Unfalsifiable provenance. Verifiable builds: build system is resistant to extra threats, prevents tampering during the build.
* SLSA Level 4: Two-person change review and [hermetic builds](../dev-eng/hermetic%20building.md). The former allows to mitigate insider threats and the latter guarantees that provenance of all dependencies can be provided. Hermeticity usually implies build reproducibility, which is desirable at SLSA level 5, but not strictly mandated. Verifiable source, prevents tampering prior to build.

On the producer side, complying to these levels lets artifact providers to indicate the level of security they can guarantee. On the consumer side, the artifact consumer can determine to what extent a particular artifact could be trusted. These levels are incremental, in the sense that being at a level *n*, there is a straighforward path to add compliance with level *n+1*.

#infosec, #supply-chain-security