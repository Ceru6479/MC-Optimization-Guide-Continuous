# This section covers Java versions for each of the supported versions of Minecraft.

| Table of contents |
|:---:|
| [1. Picking a Java version](#picking-a-java-version) |
| [2. JVM Arguments](#jvm-arguments) |

# Picking a Java version

## 1.20.1+
| Mod Loader | Java | Notes |
|:---:|:---:|:---:|
| Fabric | [Adoptium Java 25](https://adoptium.net/temurin/releases/?version=25&package=jre) | - |
| Forge/NeoForge | [Adoptium Java 25](https://adoptium.net/temurin/releases/?version=25&package=jre) | - |
| Forge | [Adoptium Java 21](https://adoptium.net/temurin/releases/?version=21&package=jre) | Use ONLY if you have a mod which doesn't work with Java 25 |

## 1.18.2 & 1.19.2
| Mod Loader | Java | Notes |
|:---:|:---:|:---:|
| Fabric | [Adoptium Java 25](https://adoptium.net/temurin/releases/?version=25&package=jre) | - |
| Forge | [Adoptium Java 24](https://adoptium.net/temurin/releases/?version=24&package=jre) | Compact Object Headers & Generational Shenandoah are experimental and may be unstable. |

## 1.16.5
| Mod Loader | Java | Notes |
|:---:|:---:|:---:|
| Fabric | [Adoptium Java 25](https://adoptium.net/temurin/releases/?version=25&package=jre) | - |
| Forge | [Adoptium Java 21](https://adoptium.net/temurin/releases/?version=21&package=jre) | I highly recommend using [these JVM arguments](https://github.com/embeddedt/ModernFix/wiki/1.16---required-arguments-for-Java-17), as well as [NashornCompatLayer](https://github.com/embeddedt/NashornCompatLayer/releases) |
| Fabric/Forge | [Adoptium Java 8](https://adoptium.net/temurin/releases/?version=8&package=jre) | Use ONLY if you have a mod which doesn't work with Java 21 or 25 |

## 1.12.2
| Mod Loader | Java | Notes |
|:---:|:---:|:---:|
| Cleanroom | [Adoptium Java 25](https://adoptium.net/temurin/releases/?version=25&package=jre) | - |

## 1.7.10
| Mod Loader | Java | Notes |
|:---:|:---:|:---:|
| Forge | [Adoptium Java 25](https://adoptium.net/temurin/releases/?version=25&package=jre) | Requires [LWJGL3ify](https://modrinth.com/mod/lwjgl3ify) |

# JVM Arguments

Depending on the Java version, different JVM arguments are available. Here's what I usually use:

| Java version | JVM arguments |
|:---:|:---:|
| Java 25 & 24 | `-XX:+UseCompactObjectHeaders -XX:+UseShenandoahGC -XX:ShenandoahGCMode=generational` |
| Java 21 & 8 | `-XX:+UseG1GC -XX:+UseStringDeduplication` |

**NOTE:** If you have an old CPU or less than 16 GB of total system RAM (like I do), I wouldn't recommend using ZGC. G1GC is a better option for such systems.

Brief explanation of what these arguments do:

`-XX:+UseG1GC` - Enables the G1 Garbage Collector. G1 is the default since Java 9, so the arg is only necessary on Java 8.

`-XX:+UseStringDeduplication` - Removes strings that share the same purpose, may increase stutters slightly. Not available on Shenandoah.

`-XX:+UseShenandoahGC` - Enables the Shenandoah Garbage Collector. It uses less overhead than Z & stutters less than G1.

`-XX:ShenandoahGCMode=generational` - Makes Shenandoah Generational. Improves performance drastically!

`-XX:+UseCompactObjectHeaders` - Enables Compact Object Headers. This feature reduces RAM usage and boosts performance a bit.

`-XX:+UnlockExperimentalVMOptions` - Enables experimental VM options.

### Additional JVM arguments

`-Djava.locale.providers=JRE` Fixes `NNBSP` characters ( ) showing up in DateFormat outputs (e.g. near timestamps) on some versions when using Java 20 or newer.

`-XX:+UseZGC` - Enables the Z Garbage Collector. It uses more RAM & worsens performance but eliminates GC-related stutters. I don't use it personally.

`-XX:+ZGenerational` - Makes ZGC generational, made default by Java 23.
