## Player Statistics API

**Purpose**: Centralize the collection, storage, and retrieval of player statistics across all minigames.

## Key Features
1. **Data Collection**
   - Track statistics such as:
     - Games played, wins, and losses.
     - Time spent in each minigame.
     - Points scored, objectives completed, or other minigame-specific metrics.
   - Store raw and aggregated data for flexible reporting.

2. **Player Profiles**
   - Maintain a centralized profile for each player with cumulative stats across all minigames.
   - Include metadata like join date, favorite minigame, or highest rank achieved.

3. **Game-Specific Stats**
   - Allow minigames to report their unique stats (e.g., kills in PvP, blocks placed in a building competition).
   - API endpoints for submitting and retrieving minigame-specific data.

4. **Leaderboards**
   - Generate global, per-minigame, or custom leaderboards based on specific metrics (e.g., top scorers, fastest completion times).
   - Allow filtering by timeframe (e.g., weekly, monthly, all-time).

5. **Real-Time Updates**
   - Enable real-time updating of statistics during gameplay, useful for live dashboards or spectator modes.

6. **Analytics and Insights**
   - Provide aggregate statistics for server admins, such as the popularity of different minigames or average player performance.
   - Expose trends like player retention or progression rates.

## Implementation Notes
- **Database Design**: Use a relational database to store statistics.
- **Performance Optimization**: Cache frequently requested data like leaderboards to reduce database queries.
- **Minigame Integration**: Provide an SDK or library that minigames can use to easily report stats to the API.
- Statistics are stored as key value pairs on a "Minigame object", each player has their own set of key value paris for every minigame. Minigame objects will control which keys are available and determine the structure / type of the value.
