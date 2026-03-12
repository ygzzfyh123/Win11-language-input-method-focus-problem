# Win11-language-input-method-focus-problem
本脚本用于windows11特有的bug处理方式，使用我的脚本来避免复制粘贴后出现莫名哐哐和英文情况！先去网上自行安装Autohotkey然后来我这里下载我的脚本管理员运行即可，开机自启需要创建快捷方式属性高级管理员然后放到启动文件夹！
此bug已通过我和多人反馈得到了官方的解决，如果你是21H2以上的版本请去下面这些链接安装msu补丁，如果你是21H2及以下那么可以继续用我的脚本！Thanks.！（注意：24H2已内置该补丁的平替版本不需要安装新的补丁，更新windows即可）
25年10月15日：我发现微软并没有根治此问题，但你仍可尝试使用下方的补丁，这可以减少问题出现的次数但还是有。此仓库解除归档状态，我会继续更新此脚本给大家带来好的体验！
26年3月10日：我发现现在新版本中此bug只会在同窗口内复制粘贴出现，跨窗口改变了焦点后不会有此问题了
26年3月12日：现在有一种新方法，通过修改注册表把触摸键盘的最后开启时间设置一个未来的时间戳，让windows认为没开启过触摸键盘。最下面有powershell脚本代码

23H2：https://www.catalog.update.microsoft.com/Search.aspx?q=KB5058405&utm_source=chatgpt.com

23H2,22H2: https://www.catalog.update.microsoft.com/Search.aspx?q=KB5058405&utm_source=chatgpt.com

23H2,22H2: https://catalog.update.microsoft.com/Search.aspx?q=KB5058405+23H2&utm_source=chatgpt.com

23H2,22H2: [https://catalog.update.microsoft.com/Search.aspx?q=KB5058405+23H2&utm_source=chatgpt.com]

23H2,22H2: https://www.catalog.update.microsoft.com/Search.aspx?q=KB5065431&utm_source=chatgpt.com

23H2,22H2: https://www.catalog.update.microsoft.com/Search.aspx?q=KB5065431&utm_source=chatgpt.com

23H2,22H2: https://www.catalog.update.microsoft.com/Search.aspx?q=KB5065431&utm_source=chatgpt.com

请选择对应你的系统版本号




$regPath = "HKCU:\Software\Microsoft\InputMethod\Settings\Common"
$regName = "InputPanelPageLastOpenTime"
$futureTimestamp = 2051193600  # 对应大约 2035 年 1 月 1 日左右，可改成更大值如 2147483647（最大 DWORD）

if (-not (Test-Path $regPath)) {
    New-Item -Path $regPath -Force | Out-Null
    Write-Host "已创建注册表路径: $regPath"
}


Set-ItemProperty -Path $regPath -Name $regName -Value $futureTimestamp -Type DWord -Force

Write-Host "已将 $regName 设置为 $futureTimestamp"
Write-Host "操作完成！请重启电脑或注销后测试输入法。"


Get-ItemProperty -Path $regPath -Name $regName
