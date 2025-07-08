nano ~/.tmux.conf
use xsel with it
# Enable AltGr + number (use M-1 for AltGr + 1, etc.)
bind -n M-1 select-window -t 1
bind -n M-2 select-window -t 2
bind -n M-3 select-window -t 3
bind -n M-4 select-window -t 4
bind -n M-5 select-window -t 5
bind -n M-6 select-window -t 6
bind -n M-7 select-window -t 7
bind -n M-8 select-window -t 8
bind -n M-9 select-window -t 9

set -g status off



set -g set-titles off
set -g mouse on
bind-key -n C-v paste-buffer
set-option -g mode-style "bg=black,fg=white"

# ~/.tmux.conf
set -g set-clipboard on  # Enable clipboard access

# Auto-copy when mouse selection ends (works in normal mode)
bind -n MouseDragEnd1Pane if-shell -F "#{mouse_any_flag}" {
    send-keys -X copy-pipe-and-cancel "xsel -i --clipboard"
}

# Auto-copy in copy-mode (for keyboard selection)
bind -T copy-mode-vi MouseDragEnd1Pane send-keys -X copy-pipe-and-cancel "xsel >
bind -T copy-mode MouseDragEnd1Pane send-keys -X copy-pipe-and-cancel "xsel -i >





TMUX BASH AUTO ATTACH

# Auto-start or attach tmux on terminal launch
if command -v tmux &> /dev/null && [ -z "$TMUX" ]; then
    tmux attach -t default || tmux new -s default
fi
