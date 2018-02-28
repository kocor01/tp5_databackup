# tp5_databackup
THINKPHP5 数据库备份还原

# 初始化
$this->config = [
    'path'     => RUNTIME_PATH.'/Backup/',//数据库备份路径
    'part'     => 20971520,//20M 数据库备份卷大小
    'compress' => 1,//数据库备份文件是否启用压缩 0不压缩 1 压缩
    'level'    => 9 //数据库备份文件压缩级别 1普通 4 一般  9最高
];

# 数据库表列表
$backup = new BackupModel($this->config);
$tableList = $backup->dataList();

# 备份
$backup = new BackupModel($this->config);
foreach ($tableList as $key => $value) {
    $start= $backup->backup($value, 0);
    if($start !== 0){
        bleak;
    }
}

# 还原
$backup = new BackupModel($this->config);
$file = ['name' => date('Ymd-His',$time), 'part' => ($part)];
$backup->setFile($file)->import($compress);

# 删除
$time = Request::instance()->param('time/s');
$backup = new BackupModel($this->config);
$tableList = $backup->delFile($time);

# 下载
$backup = new BackupModel($this->config);
$tableList = $backup->downloadFile($time,$part);