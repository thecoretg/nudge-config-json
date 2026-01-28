
# Nudge Config JSON

Configuration files for [Nudge](https://github.com/macadmins/nudge). Called by MDM configuration profiles.

## Universal Settings

### Expected Behavior

Nudge will not prompt if:

- Camera is active
- Screen sharing is active

Nudge will enforce, at a minimum, the latest minor version of the OS of the device. If the device is on a "No Major Deferrals" profile, it will enforce both the latest major and minor version.

### Refresh Cycles

- Initial
  - Window: >72 Hours from Deadline
  - Prompt Interval: 5 Hours
- Approaching
  - Window: <72 Hours from Deadline
  - Prompt Interval: 2 Hours
- Imminent
  - Window: <24 Hours from Deadline
  - Prompt Interval: 15 Minutes
- Elapsed
  - Window: Past Deadline
  - Prompt Interval: 5 Minutes

### Deadlines

The given deadline before a device reaches the Elapsed window is determined by the security updates in the latest update.

If an update only provides feature and quality updates and has minimal security content, the deadline will be longer.

The start date of the deadline, at a baseline, is the day Apple released the update. The following numbers show the deadline from release based on CVE. We use Nudge's default numbers for this.

- Standard Update (No Security Urgency): 28 days
- Non Actively Exploited CVE: 21 days
- Actively Exploited CVE: 14 days

For example, if Apple releases an update and it has security patches that are actively exploited, the user will have 14 days to install the update before the window elapses.

### Deployment Groups

In an effort to not push updates to all clients at once, we have 5 separate profiles with a number of days offset from the default deadlines above.

These profiles are assigned to orgs spread out to be balanced. In cases where critical, high-profile CVEs are included in a released update, we temporarily move all orgs to the lowest deadline group. As of writing this, we have not run into a situation like this.

These offsets apply to update visibility and deadlines.

For example, if an org is in the 10 day group, a visibility delay of 10 days is applied, and the deadline days are increased by 10 so it is, from lowest to highest severity, 38, 31, and 24 day deadlines (as opposed to the default of 28, 21, and 14).
