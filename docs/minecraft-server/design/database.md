# Database Models

## 1. Players
Stores centralised information about each player.

| Column Name       | Type         | Description                                     |
|-------------------|--------------|-------------------------------------------------|
| `id`              | UUID         | Unique identifier for the player's Minecraft account. |
| `miners_online_id` | UUID        | Unique identifier for the player's Miners Online account. |
| `username`        | VARCHAR(255) | The player’s username.                         |
| `join_date`       | TIMESTAMP    | Date and time the player joined.               |
| `metadata`        | JSONB        | Additional metadata (e.g., preferences).       |
| `created_at`      | TIMESTAMP    | Timestamp when the profile was created.        |
| `updated_at`      | TIMESTAMP    | Last update timestamp.                         |


## 2. Minigames
Defines each minigame and its allowed statistic keys.

| Column Name       | Type         | Description                                     |
|-------------------|--------------|-------------------------------------------------|
| `id`              | UUID         | Unique identifier for the minigame.            |
| `name`            | VARCHAR(255) | Minigame name.                                 |
| `description`     | TEXT         | Description of the minigame.                   |
| `stat_keys`       | JSONB        | Defines allowed statistic keys and types (e.g., kills: INT, time_played: FLOAT). |
| `created_at`      | TIMESTAMP    | Timestamp when the minigame was added.         |
| `updated_at`      | TIMESTAMP    | Last update timestamp.                         |


## 3. Player_Stats
Stores statistics for each player and minigame.

| Column Name       | Type         | Description                                     |
|-------------------|--------------|-------------------------------------------------|
| `id`              | UUID         | Unique identifier for the stat entry.          |
| `player_id`       | UUID         | Foreign key referencing `players.id`.          |
| `minigame_id`     | UUID         | Foreign key referencing `minigames.id`.        |
| `stats`           | JSONB        | Key-value pairs of stats (e.g., `{"kills": 10, "time_played": 360.5}`). |
| `created_at`      | TIMESTAMP    | Timestamp when the stats were created.         |
| `updated_at`      | TIMESTAMP    | Last update timestamp.                         |


## 4. Leaderboards
Pre-computed leaderboard data for fast access.

| Column Name       | Type         | Description                                     |
|-------------------|--------------|-------------------------------------------------|
| `id`              | UUID         | Unique identifier for the leaderboard.         |
| `minigame_id`     | UUID         | Foreign key referencing `minigames.id`.        |
| `metric`          | VARCHAR(255) | The leaderboard metric (e.g., "kills", "time_played"). |
| `timeframe`       | VARCHAR(50)  | Leaderboard timeframe (e.g., "weekly", "all-time"). |
| `data`            | JSONB        | Array of leaderboard entries (e.g., `[{player_id: UUID, score: INT}]`). |
| `last_generated`  | TIMESTAMP    | Timestamp of the last update.                  |


## 5. Analytics
Aggregated analytics for server admins.

| Column Name       | Type         | Description                                     |
|-------------------|--------------|-------------------------------------------------|
| `id`              | UUID         | Unique identifier for the analytics entry.     |
| `metric`          | VARCHAR(255) | The aggregated metric name (e.g., "thing.popularity"). |
| `data`            | VARCHAR(255) | Aggregated data.                               |
| `created_at`      | TIMESTAMP    | Timestamp when the analytics were generated.   |

## Relationships
1. **Players ↔ Player_Stats**:
   - One-to-many relationship where `Player_Stats` tracks individual player stats for each minigame.

2. **Minigames ↔ Player_Stats**:
   - One-to-many relationship to associate stats with specific minigames.

3. **Minigames ↔ Leaderboards**:
   - One-to-many relationship to store leaderboard data for each minigame.

## Key Features Support

1. **Flexible Key-Value Statistics**:
   - `Player_Stats.stats` stores minigame-specific data as JSONB for dynamic key-value flexibility.

2. **Cumulative Stats**:
   - Use SQL or application logic to aggregate `Player_Stats.stats` for each player.

3. **Real-Time Updates**:
   - `Player_Stats.updated_at` allows tracking the last update, enabling real-time dashboards.

4. **Leaderboards**:
   - Pre-compute leaderboards in the `Leaderboards` table for performance optimisation.

5. **Analytics**:
   - Use `Analytics` to store aggregated data for admin insights.
