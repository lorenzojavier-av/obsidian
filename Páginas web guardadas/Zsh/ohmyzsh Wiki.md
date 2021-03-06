To try it out if you have just cloned it (to your home directory):

source ~/.oh-my-zsh/templates/zshrc.zsh-template

___

## Commands

Command

Description

_alias_

list all aliases

_tabs_

Create a new tab in the current directory (macOS - requires enabling access for assistive devices under System Preferences).

_take_

Create a new directory and change to it, will create intermediate directories as required.

_x_ / _extract_

Extract an archive (supported types: tar.{bz2,gz,xz,lzma}, bz2, rar, gz, tar, tbz2, tgz, zip, Z, 7z).

_zsh\_stats_

Get a list of the top 20 commands and how many times they have been run.

_uninstall\_oh\_my\_zsh_

Uninstall Oh-my-zsh.

_omz update_

Upgrade Oh-my-zsh.

`exec zsh`

Apply changes made to zshrc

___

### Alias

Flag

Description

L

print each alias in the form of calls to alias

g

list or define global aliases

m

print aliases matching specified pattern

r

list or define regular aliases

s

list or define suffix aliases

## Tab-completion

For options and helpful text of what they do

_ls -(tab)_

_cap (tab)_

_rake (tab)_

_ssh (tab)_

_sudo umount (tab)_

_kill (tab)_

_unrar (tab)_

## Directory

Alias

Command

..

cd ..

...

cd ../..

....

cd ../../..

.....

cd ../../../..

/

cd /

~

cd ~

_cd +n_

switch to directory number `n`

_\-_

cd -

_1_

cd -

_2_

cd -2

_3_

cd -3

_4_

cd -4

_5_

cd -5

_6_

cd -6

_7_

cd -7

_8_

cd -8

_9_

cd -9

_md_

mkdir -p

_rd_

rmdir

_d_

dirs -v (lists last used directories)

See `~/.oh-my-zsh/lib/directories.zsh`

## Git

Alias

Command

_g_

git

_ga_

git add

_gau_

git add --update (Also: "git add -u")

_gaa_

git add --all

_gapa_

git add --patch

_gb_

git branch

_gba_

git branch -a

_gbd_

git branch -d

_gbda_

git branch --no-color --merged | command grep -vE "^(+|\*|\\s\*($(git\_main\_branch)|development|develop|devel|dev)\\s\*$)" | command xargs -n 1 git branch -d

_gbl_

git blame -b -w

_gbnm_

git branch --no-merged

_gbr_

git branch --remote

_gbs_

git bisect

_gbsb_

git bisect bad

_gbsg_

git bisect good

_gbsr_

git bisect reset

_gbss_

git bisect start

_gc_

git commit -v

_gc!_

git commit -v --amend

_gca_

git commit -v -a

_gca!_

git commit -v -a --amend

_gcan!_

git commit -v -a --no-edit --amend

_gcans!_

git commit -v -a -s --no-edit --amend

_gcam_

git commit -a -m

_gcsm_

git commit -s -m

_gcb_

git checkout -b

_gcf_

git config --list

_gcl_

git clone --recurse-submodules

_gclean_

git clean -id

_gpristine_

git reset --hard && git clean -dffx

_gcm_

git checkout $(git\_main\_branch)

_gcd_

git checkout develop

_gcmsg_

git commit -m

_gco_

git checkout

_gcount_

git shortlog -sn

_gcp_

git cherry-pick

_gcpa_

git cherry-pick --abort

_gcpc_

git cherry-pick --continue

_gcs_

git commit -S

_gd_

git diff

_gdca_

git diff --cached

_gdct_

git describe --tags \`git rev-list --tags --max-count=1\`

_gds_

git diff --staged

_gdt_

git diff-tree --no-commit-id --name-only -r

_gdw_

git diff --word-diff

_gf_

git fetch

_gfa_

git fetch --all --prune

_gfo_

git fetch origin

_gg_

git gui citool

_gga_

git gui citool --amend

_ggpnp_

git pull origin $(current\_branch) && git push origin $(current\_branch)

_ggpull_

git pull origin $(current\_branch)

_ggl_

git pull origin $(current\_branch)

_ggpur_

git pull --rebase origin $(current\_branch)

_ggu_

git pull --rebase origin $(current\_branch)

_glum_

git pull upstream $(git\_main\_branch)

_ggpush_

git push origin $(current\_branch)

_ggp_

git push origin $(current\_branch)

_ggfl_

git push --force-with-lease origin <your\_argument>/$(current\_branch)

_ggsup_

git branch --set-upstream-to=origin/$(current\_branch)

_gpsup_

git push --set-upstream origin $(current\_branch)

_ghh_

git help

_gignore_

git update-index --assume-unchanged

_gignored_

git ls-files -v

_git-svn-dcommit-push_

git svn dcommit && git push github master:svntrunk

_gk_

\\gitk --all --branches

_gke_

\\gitk --all $(git log -g --pretty=%h)

_gl_

git pull

_glg_

git log --stat

_glgg_

git log --graph

_glgga_

git log --graph --decorate --all

_glgm_

git log --graph --max-count=10

_glgp_

git log --stat -p

_glo_

git log --oneline --decorate

_glog_

git log --oneline --decorate --graph

_glol_

git log --graph --pretty=\\'%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset\\'

_glola_

git log --graph --pretty=\\'%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset\\' --all

_glp_

\_git\_log\_prettily (Also: "git log --pretty=$1")

_gm_

git merge

_gma_

git merge --abort

_gmom_

git merge origin/$(git\_main\_branch)

_gmt_

git mergetool --no-prompt

_gmtvim_

git mergetool --no-prompt --tool=vimdiff

_gmum_

git merge upstream/$(git\_main\_branch)

_gp_

git push

_gpd_

git push --dry-run

_gpoat_

git push origin --all && git push origin --tags

_gpu_

git push upstream

_gpv_

git push -v

_gr_

git remote

_gra_

git remote add

_grb_

git rebase

_grba_

git rebase --abort

_grbc_

git rebase --continue

_grbd_

git rebase develop

_grbi_

git rebase -i

_grbm_

git rebase $(git\_main\_branch)

_grbs_

git rebase --skip

_grh_

git reset (Also: "git reset HEAD")

_grhh_

git reset --hard (Also: "git reset HEAD --hard")

_grmv_

git remote rename

_grrm_

git remote remove

_grs_

git restore

_grset_

git remote set-url

_grt_

cd $(git rev-parse --show-toplevel || echo ".")

_gru_

git reset --

_grup_

git remote update

_grv_

git remote -v

_gsb_

git status -sb

_gsd_

git svn dcommit

_gsi_

git submodule init

_gsps_

git show --pretty=short --show-signature

_gsr_

git svn rebase

_gss_

git status -s

_gst_

git status

_gsta_

git stash push

_gstaa_

git stash apply

_gstd_

git stash drop

_gstl_

git stash list

_gstp_

git stash pop

_gstc_

git stash clear

_gsts_

git stash show --text

_gsu_

git submodule update

_gsw_

git switch

_gswc_

git switch -c

_gts_

git tag -s

_gunignore_

git update-index --no-assume-unchanged

_gunwip_

git log -n 1 | grep -q -c "--wip--" && git reset HEAD~1

_gup_

git pull --rebase

_gupv_

git pull --rebase -v

_gvt_

git verify-tag

_gwch_

git whatchanged -p --abbrev-commit --pretty=medium

_gwip_

git add -A; git rm $(git ls-files --deleted) 2> /dev/null; git commit --no-verify --no-gpg-sign -m "--wip-- \[skip ci\]"

Dynamic access to current branch name with the current\_branch function

git pull origin $(current\_branch)

grb publish $(current\_branch) origin

You also find these commands in Dash as a Cheat-sheet.

## Editors

Alias

Command

_stt_

(When using `sublime` plugin) Open current directory in Sublime Text 2/3

_v_

(When using `vi-mode` plugin) Edit current command line in Vim

## Symfony2

Alias

Command

_sf_

php ./app/console

_sfcl_

php app/console cache:clear

_sfcontainer_

sf debug:container

_sfcw_

sf cache:warmup

_sfgb_

sf generate:bundle

_sfroute_

sf debug:router

_sfsr_

sf server:run -vvv

## tmux

Alias

Command

_ta_

tmux attach -t

_tad_

tmux attach -d -t

_ts_

tmux new-session -s

_tl_

tmux list-sessions

_tksv_

tmux kill-server

_tkss_

tmux kill-session -t

## Systemd

### systemctl

Command

Description

_sc-status NAME_

show the status of the NAME process

_sc-show NAME_

show the NAME systemd .service file

_sc-start NAME_

start the NAME process

_sc-stop NAME_

stop the NAME process

_sc-restart NAME_

restart the NAME process

_sc-enable NAME_

enable the NAME process to start at boot

_sc-disable NAME_

disable the NAME process at boot

## Rails

### Rails Aliases

Alias

Command

_rc_

rails console

_rcs_

rails console --sandbox

_rd_

rails destroy

_rdb_

rails dbconsole

_rg_

rails generate

_rgm_

rails generate migration

_rp_

rails plugin

_ru_

rails runner

_rs_

rails server

_rsd_

rails server --debugger

_rsp_

rails server --port

### RAILS\_ENV Aliases

Alias

Command

_RED_

RAILS\_ENV=development

_REP_

RAILS\_ENV=production

_RET_

RAILS\_ENV=test

## zoxide

Command

Description

`z foo`

`cd` into highest ranked directory matching `foo`

`z foo bar`

`cd` into highest ranked directory matching `foo` and `bar`

`z ~/foo`

`z` also works like a regular `cd` command

`z foo/`

`cd` into relative path

`z ..`

`cd` one level up

`z -`

`cd` into previous directory

`zi foo`

`cd` with interactive selection (using `fzf`)