# Minecraft Helm Chart

This helm chart runs Minecraft 1.18 off of Kubernetes! Configure it at your own will:

```yaml
# Server configuration, including download URLs for binaries and JVM configuration
server:
  # arguments for the JVM
  args: -Xmx3000M -Xms1024M -jar
  # commands with which to start the server
  command: nogui
  jar:
    # download URL for minecraft server jar
    url: "https://launcher.mojang.com/v1/objects/3cf24a8694aca6267883b17d934efacc5e44440d/server.jar"
  mcrcon:
    # download URL for mcrcon
    url: "https://github-releases.githubusercontent.com/10777685/691c62a4-407c-417c-96c6-40ae8e504b2e?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20211130%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211130T221541Z&X-Amz-Expires=300&X-Amz-Signature=9befa22db0764be9163d6830ee0d9d2690782df1d5e428af05910807fb1a2425&X-Amz-SignedHeaders=host&actor_id=16052098&key_id=0&repo_id=10777685&response-content-disposition=attachment%3B%20filename%3Dmcrcon-0.7.2-linux-x86-64.tar.gz&response-content-type=application%2Foctet-stream"
  config:
    # default gamemode
    gamemode: survival
    # level name
    levelName: world
    # initial level seed for world generation
    seed: "-7497863297697545553"
    # message of the day
    motd: A Minecraft Server
    # whether or not PVP should be enabled
    pvp: true
    # difficulty, either peaceful, easy, normal, or hard
    difficulty: easy
    # hardcore mode
    hardcore: false
    rendering:
      # chunk distance property, i.e., how far should chunks be served to a player
      viewDistance: 10
      simulationDistance: 10
    server:
      # server-ip
      host: 0.0.0.0
      # server port
      port: 25565
      # rate-limit, 0 is no limit at all
      rateLimit: 0
      # whether or not commands from console should be broadcast to OPs
      broadcastConsoleToOPs: true
      # prevents players behind proxys from connecting
      preventProxyConnections: false
    game:
      # max-player property
      maxPlayers: 20
      # online-mode property, will only allow authenticated players to join the server
      onlineMode: true
      # enable-command-block property
      enableCommandBlock: false
      # enabled-status
      enableStatus: true
      # allow-flight
      allowFlight: true
      # max-time-time
      maxTickTime: 60000
      # max-world-size
      maxWorldSize: 29999984
      # spawn-protection
      spawnProtection: 16
      # force-gamemode
      forceGamemode: false
      # player-idle-timeout
      playerIdleTimeout: 0
      # allow-nether
      allowNether: true
      # hide-online-players
      hideOnlinePlayers: false
      # spawn properties
      spawn:
        monsters: true
        animals: true
        npcs: true
    # rcon properties for the minecraft server
    rcon:
      # whether or not rcon is enabled. NOTE that we need this for lifecycle hooks
      enabled: true
      # default rcon ports
      port: 25575
      password: "" # if this is empty, we will generate one randomly for you!
      # whether or not to broadcast rcon events to OPs
      broadcastToOPs: true
    io:
      syncChunkWrites: true
      networkCompressionThreshold: 256
      useNativeTransport: true
    # resource pack configuration
    resourcePack:
      pack: ""
      require: true
      sha1: ""
      prompt: ""
    # query configuration for inbound traffic
    query:
      enabled: true
      port: 25565
    # permission level for executing commands
    permissionLevel:
      op: 4
      function: 2
    # whether or not whitelists should be enabled
    whitelist:
      enabled: true
    advanced:
      enableJMXMonitoring: false
      entityBroadcastRangePercentage: 100
```

## Installation

```bash
helm repo add zoomoid https://zoomoid.github.io/iron-helm
helm repo update

# install it
helm install my-server zoomoid/minecraft -f values.yaml
```
