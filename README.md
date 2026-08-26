# WezTerm.lua

`
local wezterm = require("wezterm")
local config = wezterm.config_builder()

----------------------------------------------------
-- 基本設定
----------------------------------------------------

-- 保存時に設定を自動反映
config.automatically_reload_config = true

-- 起動時にWSL Ubuntuを開く
config.default_domain = "WSL:Ubuntu"

-- フォントサイズ
config.font_size = 13.0

-- 日本語入力
config.use_ime = true

----------------------------------------------------
-- 背景画像
----------------------------------------------------

config.background = {
  {
    source = {
      File = wezterm.config_dir .. "/background.jpg",
    },

    width = "Cover",
    height = "Cover",

    repeat_x = "NoRepeat",
    repeat_y = "NoRepeat",

    horizontal_align = "Center",
    vertical_align = "Middle",

    -- 画像を暗くして文字を見やすくする
    hsb = {
      brightness = 0.25,
      saturation = 0.9,
    },
  },
}

----------------------------------------------------
-- ウィンドウ
----------------------------------------------------

-- Windows標準タイトルバーを非表示
config.window_decorations = "RESIZE"

-- カスタムタブを使用
config.use_fancy_tab_bar = false

-- Windowsの背景効果
config.win32_system_backdrop = "Acrylic"

----------------------------------------------------
-- タブバー
----------------------------------------------------

config.show_tabs_in_tab_bar = true

-- タブが1つでも表示する
config.hide_tab_bar_if_only_one_tab = false

-- ＋ボタンを非表示
config.show_new_tab_button_in_tab_bar = false

-- タブバーを透明化
config.window_frame = {
  inactive_titlebar_bg = "none",
  active_titlebar_bg = "none",
}

config.colors = {
  tab_bar = {
    background = "rgba(0, 0, 0, 0)",
    inactive_tab_edge = "none",
  },
}

----------------------------------------------------
-- タブタイトル
----------------------------------------------------

local SOLID_LEFT_ARROW =
  wezterm.nerdfonts.ple_lower_right_triangle

local SOLID_RIGHT_ARROW =
  wezterm.nerdfonts.ple_upper_left_triangle

wezterm.on(
  "format-tab-title",
  function(tab, tabs, panes, wezterm_config, hover, max_width)
    local background = "#5c6d74"
    local foreground = "#ffffff"
    local edge_background = "rgba(0, 0, 0, 0)"

    if tab.is_active then
      background = "#ae8b2d"
    end

    local title =
      "  "
      .. wezterm.truncate_right(
        tab.active_pane.title,
        max_width - 4
      )
      .. "  "

    return {
      {
        Background = {
          Color = edge_background,
        },
      },
      {
        Foreground = {
          Color = background,
        },
      },
      {
        Text = SOLID_LEFT_ARROW,
      },
      {
        Background = {
          Color = background,
        },
      },
      {
        Foreground = {
          Color = foreground,
        },
      },
      {
        Text = title,
      },
      {
        Background = {
          Color = edge_background,
        },
      },
      {
        Foreground = {
          Color = background,
        },
      },
      {
        Text = SOLID_RIGHT_ARROW,
      },
    }
  end
)

----------------------------------------------------
-- キーバインド
----------------------------------------------------

-- Ctrl + Shift + C：コピー
-- Ctrl + Shift + V：貼り付け
-- Ctrl + Shift + T：新しいタブ

`

return config
