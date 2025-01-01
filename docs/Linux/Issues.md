# Thunar has no access to mount drives
Create following `polkit` rule for `udisks2` at `/etc/polkit-1/rules.d/10-udisks2.rules`

```
polkit.addRule(function(action, subject) {
    if ((action.id == "org.freedesktop.udisks2.filesystem-mount-system" ||
         action.id == "org.freedesktop.udisks2.filesystem-mount") &&
        subject.isInGroup("wheel")) {
        return polkit.Result.YES;
    }
});
```