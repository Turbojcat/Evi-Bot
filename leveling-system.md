# Leveling System Documentation

## Overview

The ThasiniaBot leveling system provides a comprehensive XP and leveling experience with different tiers for free, premium, and lifetime users. The system includes message XP, voice XP, streaks, rewards, badges, and advanced features.

## Core Features

### XP System
- **Message XP**: Awarded for valid messages (15 XP base)
- **Voice XP**: Awarded for speaking in voice channels (10 XP per minute)
- **Streak Bonus**: Daily activity streaks provide XP multipliers
- **Premium Multipliers**: Premium servers get enhanced XP rates

### Level Progression
- **Non-linear XP Curve**: Each level requires more XP than the previous
- **Formula**: `Math.floor(100 * Math.pow(1.5, level))`
- **No Level Cap**: Users can progress indefinitely
- **XP Carryover**: Excess XP carries over to next level

### Spam Detection & Prevention

#### Message Spam Detection
The system includes comprehensive spam detection to prevent XP abuse:

**Duplicate Message Detection:**
- Prevents XP gain from sending the same message multiple times in a row
- Case-insensitive comparison
- Tracks last message per user per server

**Random Character/Number/Symbol Spam:**
- **Minimum Requirements**: 2 words minimum, 5 characters minimum
- **Pattern Detection**: Identifies random typing patterns
- **Symbol Spam**: Blocks excessive symbols (`!@#$%^&*()` etc.)
- **Number Spam**: Blocks excessive numbers (`123456789` etc.)
- **Random String Detection**: Identifies keyboard patterns (`qwerty`, `asdfgh`, etc.)
- **Repeating Characters**: Blocks messages with 3+ same characters (`aaa`, `111`, etc.)
- **Mixed Random**: Detects alternating random patterns (`abc123def456`)

**Spam Threshold:**
- 70% spam content threshold
- Messages exceeding this threshold are blocked from XP gain

#### Voice Spam Prevention
- **Speaking Detection**: Only awards XP when user is actually speaking
- **Minimum Speaking Time**: 5 seconds minimum required
- **Cooldown System**: 1 minute cooldown between voice XP gains
- **Muted/Deafened**: No XP when user is muted or deafened

## Commands

### User Commands
- **`/rank [user]`** - View rank card for yourself or another user
- **`/leaderboard [type]`** - View leveling leaderboards
- **`/badges [user]`** - View badges (any user's badges, manage own if premium)
- **`/streak`** - View your daily streak information
- **`/voicexp`** - View voice XP settings and statistics

### Admin Commands
- **`/levelingsettings`** - Configure leveling system settings
- **`/xp add|remove <user> <amount>`** - Add/remove XP from user
- **`/level set <user> <level>`** - Set user's level directly
- **`/levelrewards set|list|remove|clear`** - Manage level rewards
- **`/levelmessage set|view|disable|test`** - Configure level-up messages
- **`/customrank set|view|remove`** - Set custom rank card backgrounds

## Premium Features

### Free Users
- Basic leveling system
- 5-10 level rewards maximum
- 10-second message XP cooldown
- Standard rank cards

### Premium Users
- Enhanced leveling features
- 20 level rewards maximum
- 5-second message XP cooldown
- Custom rank card backgrounds (non-GIF)
- Badge system access
- Advanced logging

### Lifetime Users
- All premium features
- 40 level rewards maximum
- Custom GIF rank card backgrounds
- Priority voice XP features
- Exclusive badges and rewards

## Streak System

### Daily Streaks
- **2 Streaks**: 5% XP bonus
- **3 Streaks**: 10% XP bonus
- **4 Streaks**: 15% XP bonus
- **5 Streaks**: 25% XP bonus
- **6 Streaks**: 35% XP bonus
- **7+ Streaks**: 50% XP bonus

### Streak Requirements
- Must send at least one valid message per day
- Must meet minimum word/character requirements
- Must not be flagged as spam

## Voice XP System

### How It Works
1. **Join Voice Channel**: User joins a voice channel
2. **Speaking Detection**: Bot monitors when user starts speaking
3. **Minimum Time**: User must speak for at least 5 seconds
4. **XP Calculation**: XP awarded based on speaking duration
5. **Cooldown**: 1-minute cooldown before next voice XP gain

### Voice XP Settings
- **Enable/Disable**: Server admins can toggle voice XP
- **XP Rate**: Configurable XP per minute of speaking
- **Premium Features**: Enhanced rates for premium servers

## Badge System

### Badge Types
- **Default Badge**: Cool badge matching bot's colors (pastel purple/lilac)
- **Custom Badges**: Server-specific badges
- **Achievement Badges**: Badges for milestones and achievements

### Badge Management
- **View Badges**: All users can view any user's badges
- **Manage Badges**: Premium users can manage their own badges
- **Award Badges**: Admins can award badges to users
- **Remove Badges**: Admins can remove badges from users

## Level Rewards

### Reward Types
- **Role Rewards**: Automatic role assignment
- **Balance Rewards**: Add/remove economy balance
- **Message Rewards**: Send custom messages
- **Custom Actions**: Any combination of the above

### Reward Management
- **Set Rewards**: Configure rewards for specific levels
- **List Rewards**: View all configured rewards
- **Remove Rewards**: Remove specific rewards
- **Clear Rewards**: Remove all rewards

## Rank Cards

### Default Rank Card
- **Background**: Custom background image
- **Colors**: Light turquoise/pastel purple theme
- **Information**: Level, XP, rank, streak, voice time
- **Design**: Modern, clean design

### Custom Rank Cards
- **Premium Users**: Can set custom backgrounds (non-GIF)
- **Lifetime Users**: Can use GIF backgrounds
- **Background URL**: Direct image URL required
- **Validation**: System validates image URLs

## Level-Up Messages

### Message Configuration
- **Default Message**: "🎉 Congratulations {user}! You reached level {level}!"
- **Custom Messages**: Server admins can set custom messages
- **Channel Selection**: Messages can be sent to specific channels
- **Embed Format**: All messages use embed format

### Message Placeholders
- **{user}** - User mention
- **{level}** - New level reached
- **{xp}** - Current XP in level
- **{totalxp}** - Total XP across all levels
- **{neededxp}** - XP needed for next level
- **{rank}** - User's rank position
- **{streak}** - Current streak count

## Database Structure

### Main Tables
- **`user_levels`** - User leveling data
- **`guild_leveling_settings`** - Server leveling configuration
- **`level_rewards`** - Level reward configurations
- **`user_badges`** - User badge data
- **`custom_rank_backgrounds`** - Custom rank card backgrounds

### Key Fields
- **XP Tracking**: Current XP, total XP, level
- **Voice Data**: Voice time, voice XP, last voice activity
- **Streak Data**: Streak count, last activity
- **Settings**: Cooldowns, multipliers, enabled features

## Technical Implementation

### Spam Detection Algorithm
```typescript
// Duplicate message detection
private isDuplicateMessage(content: string, userId: string): boolean {
  const lastMessage = this.userLastMessages.get(userId);
  return content.toLowerCase() === lastMessage?.toLowerCase();
}

// Random character detection
private isRandomString(str: string): boolean {
  const hasRepeatingChars = /(.)\1{2,}/.test(str);
  const hasRandomPattern = /[qwertyuiop]{3,}|[asdfghjkl]{3,}|[zxcvbnm]{3,}/i.test(str);
  const hasMixedRandom = /[a-z]{2,}[0-9]{2,}[a-z]{2,}|[0-9]{2,}[a-z]{2,}[0-9]{2,}/i.test(str);
  return hasRepeatingChars || hasRandomPattern || hasMixedRandom;
}
```

### XP Calculation
```typescript
// Non-linear XP curve
const neededXP = Math.floor(100 * Math.pow(1.5, level));

// Streak bonus calculation
const streakBonus = this.calculateStreakBonus(streakCount);
const finalXP = Math.floor(baseXP * (1 + streakBonus) * multiplier);
```

## Configuration Options

### Server Settings
- **XP Cooldown**: 5-10 seconds (premium vs free)
- **XP Multiplier**: Server-wide XP multiplier
- **Voice XP**: Enable/disable voice XP
- **Streak System**: Enable/disable streak bonuses
- **Premium Features**: Enable premium enhancements

### User Settings
- **Custom Rank Cards**: Personal rank card backgrounds
- **Badge Preferences**: Badge display preferences
- **Notification Settings**: Level-up notifications

## Future Enhancements

### Planned Features
- **Advanced Voice Features**: Voice quality detection, voice parties
- **Social Features**: Auto roles, voice challenges
- **Advanced Rewards**: More complex reward systems
- **Analytics**: Detailed leveling statistics
- **Events**: Special leveling events and competitions

### Voice Features (Documented)
- **Voice Quality Detection**: Award bonus XP for quality voice
- **Voice Duration Bonuses**: Different rates for different durations
- **Voice Patterns**: Analyze speaking patterns
- **Voice Parties**: Group sessions with bonus XP
- **Voice Challenges**: Daily/weekly voice challenges
- **Voice Competitions**: Voice activity competitions

## Support and Troubleshooting

### Common Issues
- **XP Not Gaining**: Check cooldown, spam detection, minimum requirements
- **Voice XP Issues**: Verify speaking detection, cooldown settings
- **Badge Display**: Check premium status, badge permissions
- **Rank Card Issues**: Validate background URLs, check permissions

### Debug Commands
- **`/levelingsettings`** - View current settings
- **`/voicexp`** - Check voice XP status
- **`/streak`** - View streak information
- **`/badges view`** - Check badge status

## Performance Considerations

### Optimization
- **Cooldown Caching**: In-memory cooldown tracking
- **Database Optimization**: Efficient queries and indexing
- **Memory Management**: Cleanup of old data
- **Rate Limiting**: Prevent abuse and spam

### Monitoring
- **XP Gain Tracking**: Monitor XP distribution
- **Spam Detection**: Track spam detection effectiveness
- **Performance Metrics**: Monitor system performance
- **User Activity**: Track user engagement

This leveling system provides a comprehensive and engaging experience for users while maintaining fair play through advanced spam detection and prevention mechanisms.
