# Voice XP Features

## Current Implementation

### Basic Voice XP System
- **Speaking Detection**: Only awards XP when user is actually speaking (not just in voice channel)
- **Minimum Speaking Time**: 5 seconds minimum speaking time required
- **Cooldown**: 1 minute cooldown between voice XP gains
- **XP Rate**: 10 XP per minute of speaking (configurable per server)
- **Integration**: Voice XP goes into regular XP system (not separate)

### Voice State Tracking
- **Join/Leave**: Tracks when users join/leave voice channels
- **Channel Changes**: Handles users moving between voice channels
- **Speaking State**: Monitors when users start/stop speaking
- **Muted/Deafened**: No XP when user is muted or deafened

## Premium Voice Features (Future Implementation)

### Premium Server Features
- **Reduced Cooldown**: 30 seconds cooldown instead of 1 minute
- **Higher XP Rate**: 15-20 XP per minute (configurable)
- **Voice Activity Logs**: Detailed logs of voice activity
- **Voice Leaderboards**: Separate leaderboards for voice activity
- **Voice Rewards**: Special rewards for voice activity milestones

### Lifetime Server Features
- **Custom Voice XP Rates**: Server admins can set custom XP rates
- **Voice Role Rewards**: Automatic role assignment based on voice time
- **Voice Statistics**: Advanced voice statistics and analytics
- **Voice Events**: Special voice events and challenges
- **Voice Badges**: Exclusive badges for voice activity

### User Premium Features
- **Personal Voice Stats**: Detailed personal voice statistics
- **Voice History**: Track voice activity history
- **Voice Goals**: Set and track voice activity goals
- **Voice Notifications**: Get notified about voice milestones

## Technical Implementation

### Voice Session Management
```typescript
interface VoiceSession {
  userId: string;
  guildId: string;
  channelId: string;
  startTime: number;
  lastSpeakTime: number;
  totalSpeakTime: number;
  isSpeaking: boolean;
  cooldownEnd: number;
}
```

### XP Calculation
```typescript
// Calculate XP based on speaking time
const speakMinutes = session.totalSpeakTime / 60000;
const xpToAward = Math.floor(speakMinutes * xpRate);
```

### Database Integration
- Voice XP is stored in `user_levels` table
- Voice time and XP are tracked separately
- Voice XP is added to regular XP for leveling

## Configuration Options

### Server Settings
- `voice_xp_enabled`: Enable/disable voice XP
- `voice_xp_rate`: XP earned per minute of speaking
- `premium_enabled`: Enable premium features

### User Settings
- Custom voice XP multipliers
- Voice activity preferences
- Voice notification settings

## Future Enhancements

### Advanced Voice Detection
- **Voice Quality**: Detect voice quality and award bonus XP
- **Voice Duration**: Different XP rates for different speaking durations
- **Voice Patterns**: Analyze speaking patterns for bonus XP

### Social Features
- **Voice Parties**: Group voice sessions with bonus XP
- **Voice Challenges**: Daily/weekly voice challenges
- **Voice Competitions**: Voice activity competitions

### Integration Features
- **Discord Events**: Integration with Discord events
- **Streaming**: XP for streaming activities
- **Stage Channels**: Special XP for stage channel activities
