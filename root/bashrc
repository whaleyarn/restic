# Browse restic snapshots with fzf and ncdu.
ncdu-restic() {
  local header snapshot

  header="$(restic snapshots --no-lock | head -n1)"
  snapshot="$(
    restic snapshots --no-lock \
      | tail -n +2 \
      | awk '{print $1 "\t" $0}' \
      | fzf --with-nth=2.. --prompt="ncdu-restic> " --header="$header" \
      | awk '{print $1}'
  )" || return

  [[ -n "$snapshot" ]] || return

  restic ls --no-lock --ncdu "$snapshot" | ncdu -f-
}
