Bạn copy – paste đoạn code sau bỏ vào functions.php nha!

// Thêm icon image vào tab trong theme Flatsome
function rflatsome_ux_builder_template( $path ) {
    ob_start();
    include get_template_directory() . '/inc/builder/shortcodes/templates/' . $path;
    return ob_get_clean();
}
//
function rflatsome_ux_builder_thumbnail( $name ) {
    return get_template_directory_uri() . '/inc/builder/shortcodes/thumbnails/' . $name . '.svg';
}
//
function giuseart_convert_name($str) {
$str = preg_replace("/(à|á|ạ|ả|ã|â|ầ|ấ|ậ|ẩ|ẫ|ă|ằ|ắ|ặ|ẳ|ẵ)/", 'a', $str);
$str = preg_replace("/(è|é|ẹ|ẻ|ẽ|ê|ề|ế|ệ|ể|ễ)/", 'e', $str);
$str = preg_replace("/(ì|í|ị|ỉ|ĩ)/", 'i', $str);
$str = preg_replace("/(ò|ó|ọ|ỏ|õ|ô|ồ|ố|ộ|ổ|ỗ|ơ|ờ|ớ|ợ|ở|ỡ)/", 'o', $str);
$str = preg_replace("/(ù|ú|ụ|ủ|ũ|ư|ừ|ứ|ự|ử|ữ)/", 'u', $str);
$str = preg_replace("/(ỳ|ý|ỵ|ỷ|ỹ)/", 'y', $str);
$str = preg_replace("/(đ)/", 'd', $str);
$str = preg_replace("/(À|Á|Ạ|Ả|Ã|Â|Ầ|Ấ|Ậ|Ẩ|Ẫ|Ă|Ằ|Ắ|Ặ|Ẳ|Ẵ)/", 'A', $str);
$str = preg_replace("/(È|É|Ẹ|Ẻ|Ẽ|Ê|Ề|Ế|Ệ|Ể|Ễ)/", 'E', $str);
$str = preg_replace("/(Ì|Í|Ị|Ỉ|Ĩ)/", 'I', $str);
$str = preg_replace("/(Ò|Ó|Ọ|Ỏ|Õ|Ô|Ồ|Ố|Ộ|Ổ|Ỗ|Ơ|Ờ|Ớ|Ợ|Ở|Ỡ)/", 'O', $str);
$str = preg_replace("/(Ù|Ú|Ụ|Ủ|Ũ|Ư|Ừ|Ứ|Ự|Ử|Ữ)/", 'U', $str);
$str = preg_replace("/(Ỳ|Ý|Ỵ|Ỷ|Ỹ)/", 'Y', $str);
$str = preg_replace("/(Đ)/", 'D', $str);
$str = preg_replace("/(\“|\”|\‘|\’|\,|\!|\&|\;|\@|\#|\%|\~|`|\=|\_|\'|\]|\[|\}|\{|\)|\(|\+|\^)/", '-', $str);
$str = preg_replace("/( )/", '-', $str);
return $str;
}
function rdev_ux_builder_element(){
add_ux_builder_shortcode('giuseart_tabs', array(
'type' => 'container',
'name' => **( 'Tab with Images' ),
'image' => '',
'category' => **( 'Content' ),
'template' => rflatsome_ux_builder_template( 'tabgroup.html' ),
'tools' => 'shortcodes/tabgroup/tabgroup.tools.html',
'info' => '{{ title }}',
'allow' => array( 'giuseart_tab' ),

        'children' => array(
            'draggable' => false,
            'addable_spots' => array( 'center' ),
        ),

        'toolbar' => array(
            'show_children_selector' => true,
            'show_on_child_active' => true,
        ),

        'presets' => array(
            array(
                'name' => __( 'Default' ),
                'content' => '
                [giuseart_tabs title="Tab Title"]
                    [giuseart_tab title="Tab 1 Title"][/giuseart_tab]
                    [giuseart_tab title="Tab 2 Title"][/giuseart_tab]
                    [giuseart_tab title="Tab 3 Title"][/giuseart_tab]
                [/giuseart_tabs]
            '
            ),
        ),

        'options' => array(

            'title' => array(
                'type' => 'textfield',
                'heading' => __( 'Title' ),
                'default' => __( '' ),
            ),

            'style' => array(
                'type' => 'select',
                'heading' => __( 'Style' ),
                'default' => 'line',
                'options' => require( get_template_directory(). '/inc/builder/shortcodes/values/nav-styles.php' ),
            ),

            'type' => array(
                'type' => 'select',
                'heading' => __( 'Type' ),
                'default' => 'horizontal',
                'options' => array(
                    'horizontal' => 'Horizontal',
                    'vertical' => 'Vertical',
                )
            ),

            'nav_style' => array(
                'type' => 'radio-buttons',
                'heading' => 'Nav Style',
                'default' => 'uppercase',
                'options' => require( get_template_directory(). '/inc/builder/shortcodes/values/nav-types-radio.php' ),
            ),

            'nav_size' => array(
                'type' => 'radio-buttons',
                'heading' => __( 'Size' ),
                'default' => 'medium',
                'options' => require( get_template_directory(). '/inc/builder/shortcodes/values/text-sizes.php' ),
            ),

            'align' => array(
                'type' => 'radio-buttons',
                'heading' => 'Tabs Align',
                'default' => 'left',
                'options' => require( get_template_directory(). '/inc/builder/shortcodes/values/align-radios.php' ),
            ),
            'bahavior_group' => array(
                'type' => 'group',
                'heading' => __( 'Behavior' ),
                'options' => array(
                    'event' => array(
                        'type'    => 'radio-buttons',
                        'heading' => __( 'Activate' ),
                        'description' => 'On hover takes effect in non-edit mode.',
                        'default' => '',
                        'options' => array(
                            ''      => array( 'title' => 'On click' ),
                            'hover' => array( 'title' => 'On hover' ),
                        ),
                    ),
                ),
            ),
            'advanced_options' => require( get_template_directory(). '/inc/builder/shortcodes/commons/advanced.php'),
        ),
    ));
    add_ux_builder_shortcode( 'giuseart_tab', array(
        'type' => 'container',
        'name' => __( ' GiuseArt Tab Panel' ),
        'template' => rflatsome_ux_builder_template('tab.html' ),
        'info' => '{{ title }}',
        'require' => array( 'giuseart_tabs' ),
        'hidden' => true,
        'wrap' => false,

        'options' => array(
            'title' => array(
                'type' => 'textfield',
                'heading' => __( 'Title' ),
                'default' => __( 'Tab Title' ),
                'auto_focus' => true,
            ),
           'img'    => array(
                'type'    => 'image',
                'heading' => 'Icon',
                'default' => '',
            ),

        ),
    ) );

}
add_action('ux_builder_setup', 'rdev_ux_builder_element');

function giuseart_tab_func($params, $content = null, $tag = ''){
$GLOBALS['tabs'] = array();
$GLOBALS['tab_count'] = 0;
$i = 1;
extract(shortcode_atts(array(
'id' => 'panel-'.rand(),
'title' => '',
'style' => 'line',
'align' => 'left',
'class' => '',
'visibility' => '',
'type' => '', // horizontal, vertical
'nav_style' => 'uppercase',
'nav_size' => 'normal',
'history' => 'false',
'event' => '',
), $params));

    if($tag == 'giuseart_tabs_vertical'){
        $type = 'vertical';
    }
    $content = do_shortcode( $content );
    $wrapper_class[] = 'tabbed-content';
    if ( $class ) $wrapper_class[] = $class;
    if ( $visibility ) $wrapper_class[] = $visibility;
    $classes[] = 'nav';
    if($style) $classes[] = 'nav-'.$style;
    if($type == 'vertical') $classes[] = 'nav-vertical';
    if($nav_style) $classes[] = 'nav-'.$nav_style;
    if($nav_size) $classes[] = 'nav-size-'.$nav_size;
    if($align) $classes[] = 'nav-'.$align;
    if($event) $classes[] = 'active-on-' . $event;
    $classes = implode(' ', $classes);
    $return = '';
    if( is_array( $GLOBALS['tabs'] )){

        foreach( $GLOBALS['tabs'] as $key => $tab ){
            if($tab['title']) $id = flatsome_to_dashed($tab['title']);
            $active = $key == 0 ? ' active' : ''; // Set first tab active by default.
            $tabs[] = '<li class="tab'.$active.' has-icon" data-code="'.giuseart_convert_name($tab['title']).'"><a href="#tab_'.giuseart_convert_name($id).'">'.flatsome_get_image( $tab['img'], 'thumbnail').'<h3>'.$tab['title'].'</h3></a></li>'; //flatsome_get_image( $tab['img'], 'thumbnail')
            $panes[] = '<div class="panel'.$active.' entry-content" id="tab_'.$id.'">'.do_shortcode( $tab['content'] ).'</div>';
            $i++;
        }
        if($title) $title = '<h4 class="uppercase text-'.$align.'">'.$title.'</h4>';
        $return = '
        <div class="'.implode(' ', $wrapper_class).' giuseart_tabs">
            '.$title.'
            <ul class="'.$classes.'">'.implode( "\n", $tabs ).'</ul><div class="tab-panels">'.implode( "\n", $panes ).'</div></div>';
    }
    return $return;

}
function giuseart_ux_tab( $params, $content = null) {
extract(shortcode_atts(array(
'title' => '',
'title_small' => '',
'img' => '',
), $params));

    $x = $GLOBALS['tab_count'];
    $GLOBALS['tabs'][$x] = array(
        'img' => $img,
        'title' => sprintf( $title, $GLOBALS['tab_count'] ),
        'content' =>  $content
    );
    $GLOBALS['tab_count']++;

}

add_shortcode('giuseart_tabs', 'giuseart_tab_func');
add_shortcode('giuseart_tabs_vertical', 'giuseart_tab_func');
add_shortcode('giuseart_tab', 'giuseart_ux_tab' );

### Bạn tạo khối UX Builder nhé. Sau đó, copy toàn bộ shortcode của block này của mình. Lưu ý: bật chế độ soạn thảo văn bản để paste dữ liệu.

###

[row class="menu-mobile"]

[col span__sm="12"]

[giuseart_tabs type="vertical" nav_style="normal"]

[giuseart_tab title="Bếp điện từ" img="1635"]

[row_inner style="small"]

[col_inner span__sm="12"]

<h3>Hãng bếp điện từ</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1667" pos="center" link="#"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo số vùng nấu</h3>
<ul>
 <li><a href="/bep-don.html"> <span class="name">Bếp điện từ đơn </span> </a></li>
 <li><a href="/bep-2-vung-nau.html"> <span class="name">2 Vùng</span> </a></li>
 <li><a href="bep-3-vung-nau.html"> <span class="name">3 Vùng</span> </a></li>
 <li><a href="/bep-4-vung-nau.html"> <span class="name">4 Vùng</span> </a></li>
 <li><a href="/bep-tu-domino.html"> <span class="name">Bếp điện từ Domino</span> </a></li>
</ul>
<h3>Sản phẩm nổi bật</h3>
<ul>
 <li><a href="/bep-tu-bosch-hmh-ppi82560ms.html"> <span class="name">Bosch PPI82560MS</span> </a></li>
 <li><a href="/bep-tu-doi-2-vung-nau-malloca-mi-732-sl.html"> <span class="name">Malloca MI 732 SL</span> </a></li>
 <li><a href="/bep-tu-2-vung-nau-ecalite-el-ms2999ii.html"> <span class="name">Ecalite EL-MS2999II</span> </a></li>
 <li><a href="//bepxanh.com/bep-1-dien-1-tu-ecalite-el-mk2688ir.html"> <span class="name">Ecalite EL-MK2688IR</span> </a></li>
</ul>
<h3>Xuất xứ</h3>
<ul>
 <li><a> <span class="name">Tây Ban Nha</span> </a></li>
 <li><a> <span class="name">Đức</span> </a></li>
 <li><a> <span class="name">Thái Lan</span> </a></li>
 <li><a> <span class="name">Malaysia</span> </a></li>
 <li><a> <span class="name">Trung Quốc</span> </a></li>
 <li><a> <span class="name">Việt Nam</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Bếp ga" img="1649"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Thương hiệu nổi tiếng</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
<ul>
 <li><a href="/bep-gas-am.html"> <span class="name">Bếp gas âm</span> </a></li>
 <li><a href="/bep-gas-duong-de-noi.html"> <span class="name">Bếp gas dương</span> </a></li>
</ul>
<h3>Số vùng nấu</h3>
<ul>
 <li><a href="/bep-gas-don.html"> <span class="name">Bếp gas đơn </span> </a></li>
 <li><a href="/bep-gas-doi.html"> <span class="name">2 vùng nấu</span> </a></li>
 <li><a href="/bep-gas-3-vung-nau.htm"> <span class="name">3 Vùng nấu </span> </a></li>
 <li><a href="/bep-gas-4-vung-nau.html"> <span class="name">4 Vùng nấu</span> </a></li>
</ul>
<h3>Xuất xứ</h3>
<ul>
 <li><a> <span class="name">Việt Nam</span> </a></li>
 <li><a> <span class="name">Italia</span> </a></li>
 <li><a> <span class="name">Trung Quốc</span> </a></li>
</ul>
<h3>Mẫu bán chạy nhất</h3>
<ul>
 <li><a href="//bepxanh.com/bep-gas-am-2-vung-nau-ecalite-eg-xd28046lcd-hen-gio-cam-ung-lcd.html"> <span class="name">Ecalite EG-XD28046LCD</span> </a></li>
 <li><a href="//bepxanh.com/bep-gas-am-3-vung-nau-ecalite-eg-xd38247b.html"> <span class="name">Ecalite EG-XD38247</span> </a></li>
 <li><a href="//bepxanh.com/bep-gas-am-1-vung-nau-ecalite-eg-xd132644b.html"> <span class="name">Ecalite EG-XD132644B</span> </a></li>
 <li><a href="//bepxanh.com/bep-gas-am-2-vung-nau-ecalite-eg-xd27545b.html"> <span class="name">Ecalite EG-XD27545B</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Máy hút mùi" img="1650"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
<ul>
 <li><a href="/may-hut-mui-am-tu.html"> <span class="name">Máy hút mùi âm tủ </span> </a></li>
 <li><a href="/may-hut-mui-co-dien-classic.html"> <span class="name">Máy hút mùi cổ điển </span> </a></li>
 <li><a href="//bepxanh.com/may-hut-mui-ap-tuong.html"> <span class="name">Máy hút mùi áp tường</span> </a></li>
 <li><a href="/may-hut-mui-dang-dao.html"> <span class="name">Máy hút mùi đảo </span> </a></li>
 <li><a href="/may-hut-mui-gia-re.html"> <span class="name">Máy hút mùi giá rẻ</span> </a></li>
</ul>
<h3>Kích thước máy hút mùi</h3>
<ul>
 <li><a href="/may-hut-mui-khu-mui.html?brand=0&amp;min=0&amp;max=0&amp;filter=:318:"> <span class="name">Ngang 60 cm</span> </a></li>
 <li><a href="/may-hut-mui-khu-mui.html?brand=0&amp;min=0&amp;max=0&amp;filter=:305:"> <span class="name">Ngang 70 cm</span> </a></li>
 <li><a href="/may-hut-mui-khu-mui.html?brand=0&amp;min=0&amp;max=0&amp;filter=:634:"><span class="name">Ngang 80 cm</span></a></li>
 <li><a href="#"> <span class="name">Ngang 90 cm</span> </a></li>
</ul>
<h3>Mẫu máy bán chạy nhất</h3>
<ul>
 <li><a href="//bepxanh.com/may-hut-mui-am-tu-h-series-ecalite-eh-at90lcd.html"> <span class="name">Ecalite EH-AT90LCD</span> </a></li>
 <li><a href="//bepxanh.com/may-hut-mui-am-tu-ngang-70cm-ecalite-eh-at700t.html"> <span class="name">Ecalite EH-AT700T</span> </a></li>
 <li><a href="//bepxanh.com/may-hut-mui-am-tu-hidden-stylish-ecalite-ehb-700lux.html"> <span class="name">Ecalite EHB-700LUX</span> </a></li>
 <li><a href="//bepxanh.com/may-hut-mui-ap-tuong-ngang-70cm-ecalite-eh-gt700t.html"> <span class="name">Ecalite EH-GT700T</span> </a></li>
 <li><a href="//bepxanh.com/may-hut-mui-am-tu-malloca-mh-700gt.html"> <span class="name">Malloca MH 700GT</span> </a></li>
 <li><a href="//bepxanh.com/may-hut-mui-classic-malloca-h3427-tc-inox-kinh-den.html"> <span class="name">Malloca H342.7 TC</span> </a></li>
 <li><a href="//bepxanh.com/may-hut-mui-am-tu-mat-kinh-den-hh-sg70a-hafele-53389021.html"> <span class="name">Hafele 533.89.021</span> </a></li>
 <li><a href="//bepxanh.com/hut-mui-bosch-hmhdwk67cm60b.html"> <span class="name">Bosch DWK67CM60B</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Chậu rửa" img="1651"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
<ul>
 <li><a href="/chau-rua-don.html"> <span class="name">Chậu rửa đơn</span> </a></li>
 <li><a href="/chau-rua-doi.html"> <span class="name">Chậu rửa đôi</span> </a></li>
 <li><a href="/chau-rua-inox.html"> <span class="name">Chậu inox</span> </a></li>
 <li><a href="/chau-rua-da-granite.html"> <span class="name">Chậu đá Granite</span> </a></li>
</ul>
<h3>Chất liệu chậu</h3>
<ul>
 <li><a href="/chau-rua-inox.html"> <span class="name">Inox 304</span> </a></li>
 <li><a href="/chau-rua-da-granite.html"> <span class="name">Đá granite</span> </a></li>
</ul>
<h3>Tính năng chậu</h3>
<ul>
 <li><a> <span class="name">1 hộc nhỏ</span> </a></li>
 <li><a> <span class="name">1 hộc lớn</span> </a></li>
 <li><a> <span class="name">2 hộc</span> </a></li>
 <li><a> <span class="name">Chậu có cánh</span> </a></li>
 <li><a> <span class="name">Có hộc dắt dao</span> </a></li>
 <li><a> <span class="name">Kèm phụ kiện</span> </a></li>
</ul>
<h3>Xuất xứ</h3>
<ul>
 <li><a> <span class="name">Trung Quốc</span> </a></li>
 <li><a> <span class="name">Hàn Quốc</span> </a></li>
 <li><a> <span class="name">Việt Nam</span> </a></li>
 <li><a> <span class="name">Malaysia</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Vòi rửa chén" img="1652"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
<ul>
 <li><a href="/voi-rua-chen-nong-lanh.html"> <span class="name">Vòi rửa chén nóng lạnh </span> </a></li>
 <li><a href="/voi-rua-chen-gia-re.html"> <span class="name">Vòi rửa chén giá rẻ</span> </a></li>
 <li><a href="//bepxanh.com/voi-rua-chen.html?brand=0&amp;min=0&amp;max=0&amp;filter=:370:"> <span class="name">Vòi dây rút</span> </a></li>
 <li><a href="//bepxanh.com/voi-rua-chen.html?brand=0&amp;min=0&amp;max=0&amp;filter=:545:"> <span class="name">Vòi kết hợp lọc nước</span> </a></li>
 <li><a href="//bepxanh.com/voi-rua-chen.html?brand=0&amp;min=0&amp;max=0&amp;filter=:543:"> <span class="name">Vòi 1 đường nước</span> </a></li>
</ul>
<h3>Chất liệu vòi</h3>
<ul>
 <li><a href="/voi-dong-thau-son-gia-da.html"> <span class="name">Đồng phủ sơn</span> </a></li>
 <li><a href="/voi-inox-304."> <span class="name">Vòi inox 304</span> </a></li>
 <li><a href="/voi-dong-thau-ma-chrome.html"> <span class="name">Đồng mạ chrome</span> </a></li>
</ul>
<h3>Sản phẩm bán chạy</h3>
<ul>
 <li><a href="//bepxanh.com/voi-rua-chen-nong-lanh-s-curve-ecalite-ef-n288s.html"> <span class="name">Ecalite EF-N288S</span> </a></li>
 <li><a href="//bepxanh.com/voi-rua-chen-nong-lanh-pan-tree-ecalite-ef-k624b.html"> <span class="name">Ecalite EF-K624B</span> </a></li>
 <li><a href="//bepxanh.com/voi-rua-chen-nong-lanh-pull-out-ecalite-ef-k541b.html"> <span class="name">Ecalite EF-K541B</span> </a></li>
 <li><a href="//bepxanh.com/voi-rua-chen-nong-lanh-silicon-ecalite-ef-k200si.html"> <span class="name">Ecalite EF-K200Si</span> </a></li>
 <li><a href="//bepxanh.com/voi-rua-chen-nong-lanh-kitchen-mixer-ecalite-ef-h013c.html"> <span class="name">Ecalite EF-H013C</span> </a></li>
 <li><a href="//bepxanh.com/voi-rua-chen-nong-lanh-kitchen-mixer-ecalite-ef-h018c.html"> <span class="name">Ecalite EF-H018C</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Máy rửa chén" img="1654"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Kiểu lắp đặt</h3>
<ul>
 <li><a href="/may-rua-chen-dung-doc-lap.html"> <span class="name">Lắp độc lập</span> </a></li>
 <li><a href="/may-rua-chen-am-tu-toan-phan.html"> <span class="name">Kiểu âm tủ</span> </a></li>
 <li><a href="/may-rua-chen-am-tu-ban-phan.html"> <span class="name">Kiểu bán âm</span> </a></li>
 <li><a href="/may-rua-chen-mini.html"> <span class="name">Kiểu mini</span> </a></li>
 <li><a href="/may-rua-chen-am-tu-toan-phan.html"> <span class="name">Kiểu âm toàn phần</span> </a></li>
</ul>
<h3>Số bộ chén rửa được</h3>
<ul>
 <li><a href="/may-rua-chen-mini.html?brand=0&amp;min=0&amp;max=0&amp;filter=:492:"> <span class="name">6 Bộ</span> </a></li>
 <li><a href="/may-rua-chen-cac-loai.html?brand=0&amp;min=0&amp;max=0&amp;filter=:467:"> <span class="name">8 đến 10 bộ</span> </a></li>
 <li><a href="/may-rua-chen-cac-loai.html?brand=0&amp;min=0&amp;max=0&amp;filter=:487:"> <span class="name">Từ 12 - 13 bộ</span> </a></li>
 <li><a href="/may-rua-chen-cac-loai.html?brand=0&amp;min=0&amp;max=0&amp;filter=:491:"> <span class="name">Trên 14 bộ</span> </a></li>
</ul>
<h3>Xuất xứ</h3>
<ul>
 <li><a> <span class="name">Đức</span> </a></li>
 <li><a> <span class="name">Trung Quốc</span> </a></li>
 <li><a> <span class="name">Thái Lan</span> </a></li>
 <li><a> <span class="name">Malaysia</span> </a></li>
 <li><a> <span class="name">Thổ Nhĩ Kỳ</span> </a></li>
 <li><a> <span class="name">Ba Lan</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Máy sấy chén" img="1656"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
<ul>
 <li><a> <span class="name">Kiểu để bàn</span> </a></li>
 <li><a href="//bepxanh.com/may-say-chen-tiet-trung.html?brand=0&amp;min=0&amp;max=0&amp;filter=:548:"> <span class="name">Kiểu treo tủ</span> </a></li>
 <li><a href="//bepxanh.com/may-say-chen-tiet-trung.html?brand=0&amp;min=0&amp;max=0&amp;filter=:547:"> <span class="name">Kiểu âm tủ</span> </a></li>
 <li><a> <span class="name">Kiểu độc lập</span> </a></li>
</ul>
<h3>Xuất xứ</h3>
<ul>
 <li><a> <span class="name">Trung Quốc</span> </a></li>
 <li><a> <span class="name">Hàn Quốc</span> </a></li>
</ul>
<h3>Mẫu bán chạy nhất</h3>
<ul>
 <li><a href="//bepxanh.com/may-say-chen-bat-tiet-trung-lap-am-tu-ecalite-ed-110c3.html"> <span class="name">Ecalite ED-110C3</span> </a></li>
 <li><a href="//bepxanh.com/may-say-tiet-trung-chen-dia-malloca-msc100a.html"> <span class="name">Malloca MSC-100A</span> </a></li>
 <li><a href="//bepxanh.com/may-say-tiet-trung-chen-dia-malloca-msc1005.html"> <span class="name">Malloca MSC-1005</span> </a></li>
 <li><a href="//bepxanh.com/may-say-chen-malloca-mdc33a.html"> <span class="name">Malloca MDC-33A</span> </a></li>
 <li><a href="//bepxanh.com/may-say-bat-cao-cap-canzy-cz-100g.html"> <span class="name">Canzy – CZ 100G</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Lò nướng" img="1657"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
<ul>
 <li><a href="/lo-nuong-am-tu.html"> <span class="name">Lắp âm tủ</span> </a></li>
 <li><a href="/lo-nuong-de-ban.html"> <span class="name">Loại để bàn</span> </a></li>
 <li><a href="/lo-nuong-ket-hop-vi-song.html"> <span class="name">Nướng kết hợp vi sóng</span> </a></li>
 <li><a href="/lo-nuong-ket-hop-lo-hap.html"> <span class="name">Nướng kết hợp hấp</span> </a></li>
</ul>
<h3>Dung tích sử dụng</h3>
<ul>
 <li><a> <span class="name">Dưới 40 Lít</span> </a></li>
 <li><a> <span class="name">Từ 40 đến 60 Lít</span> </a></li>
 <li><a> <span class="name">Trên 60Lít</span> </a></li>
</ul>
<h3>Tính năng chính</h3>
<ul>
 <li><a> <span class="name">Đối lưu</span> </a></li>
 <li><a> <span class="name">Xiên quay</span> </a></li>
 <li><a> <span class="name">Nhiệt phân</span> </a></li>
 <li><a> <span class="name">Thủy phân</span> </a></li>
</ul>
<h3>Xuất xứ</h3>
<ul>
 <li><a> <span class="name">Thái Lan</span> </a></li>
 <li><a> <span class="name">Trung Quốc</span> </a></li>
 <li><a> <span class="name">Thổ Nhĩ Kỳ</span> </a></li>
 <li><a> <span class="name">Malaysia</span> </a></li>
 <li><a> <span class="name">Đức</span> </a></li>
</ul>
<h3>Mẫu bán chạy nhất</h3>
<ul>
 <li><a href="//bepxanh.com/lo-nuong-am-tu-dung-tich-72l-ecalite-eov-ja7060bl.html"> <span class="name">Ecalite EOV-JA7060BL</span> </a></li>
 <li><a href="//bepxanh.com/lo-nuong-am-tu-ecalite-eov-ja7060ss.html"> <span class="name">Ecalite EOV-JA7060SS</span> </a></li>
 <li><a href="//bepxanh.com/lo-nuong-bosch-hbf113br0a.html"> <span class="name">Bosch HBF113BR0A</span> </a></li>
 <li><a href="//bepxanh.com/lo-nuong-am-6-chuc-nang-75l-malloca-mov-656-eco.html"> <span class="name">Malloca MOV-656 ECO</span> </a></li>
 <li><a href="//bepxanh.com/lo-nuong-am-tu-hafele-ho-4kt70a-53861442.html"> <span class="name">Hafele HO-4KT70A 538.61.442</span> </a></li>
 <li><a href="//bepxanh.com/lo-nuong-teka-hcb-6525-111020029.html"> <span class="name">Teka HCB 6525 111020029</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Máy lọc nước" img="1658"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
<ul>
 <li><a href="/may-loc-nuoc.html"> <span class="name">Máy lọc nước uống trực tiếp</span> </a></li>
 <li><a href="/cay-nuoc-nong-lanh.html"> <span class="name">Cây nước nóng lạnh</span> </a></li>
 <li><a href="/may-loc-nuoc-dien-giai.html"> <span class="name">Máy lọc nước điện giải</span> </a></li>
 <li><a href="/may-loc-nuoc-nong-lanh.html"> <span class="name">Máy lọc nước nóng lạnh</span> </a></li>
 <li><a href="/may-loc-nuoc-tao-da-vien.html"> <span class="name">Máy lọc nước tạo đá viên</span> </a></li>
 <li><a href="/loc-nuoc-van-phong-nha-xuong.html"> <span class="name">Máy lọc nước văn phòng - nhà xưởng</span> </a></li>
</ul>
<h3>Công nghệ lọc nước</h3>
<ul>
 <li><a href="/may-loc-nuoc-nano.html"> <span class="name">Nano</span> </a></li>
 <li><a href="/may-loc-nuoc-cong-nghe-uf.html"> <span class="name">UF</span> </a></li>
 <li><a href="/may-loc-nuoc-ro-tinh-khiet.html"> <span class="name">RO</span> </a></li>
 <li><a href="/may-loc-nuoc-dien-giai.html"> <span class="name">Ion kiềm</span> </a></li>
</ul>
<h3>Vị trí lắp đặt</h3>
<ul>
 <li><a href="/may-loc-nuoc-de-ban.html"> <span class="name">Để bàn</span> </a></li>
 <li><a href="/may-loc-nuoc-lap-duoi-chau.html"> <span class="name">Lắp dưới chậu</span> </a></li>
 <li><a href="/may-loc-nuoc-tai-voi.html"> <span class="name">Tại vòi</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Điện máy" img="1660"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
<ul>
 <li><a href="/tu-lanh.html"> <span class="name">Tủ lạnh</span> </a></li>
 <li><a href="/may-giat.html"> <span class="name">Máy giặt</span> </a></li>
 <li><a href="/may-hut-bui.html"> <span class="name">Máy hút bụi</span> </a></li>
 <li><a href="/may-lanh-dieu-hoa.html"> <span class="name">Máy lạnh - Điều hoà</span> </a></li>
 <li><a href="/may-xay-sinh-to.html"> <span class="name">Máy xay sinh tố</span> </a></li>
 <li><a href="/noi-com-dien.html"> <span class="name">Nồi cơm điện</span> </a></li>
 <li><a href="/may-pha-ca-phe.html"> <span class="name">Máy pha cà phê</span> </a></li>
</ul>
<h3>Mẫu bán chạy nhất</h3>
<ul>
 <li><a href="//bepxanh.com/smart-tivi-qled-4k-65-inch-samsung-qa65q80c.html"> <span class="name">Samsung QA65Q80C</span> </a></li>
 <li><a href="//bepxanh.com/may-giat-cua-truoc-10kg-ultimatecare-300-electrolux-ewf1024m3sb.html"> <span class="name">Electrolux EWF1024M3SB</span> </a></li>
 <li><a href="//bepxanh.com/tu-lanh-hitachi-inverter-569-lit-r-wb640vgv0-gmg.html"> <span class="name">Hitachi R-WB640VGV0</span> </a></li>
 <li><a href="//bepxanh.com/may-say-ngung-tu-electrolux-edc804p5wb.html"> <span class="name">Electrolux EDC804P5WB</span> </a></li>
 <li><a href="//bepxanh.com/may-giat-bosch-hmhwau28440sg-may-giat-cua-truoc-10kg-1400vp-series-6.html"> <span class="name">Bosch WAU28440SG</span> </a></li>
 <li><a href="//bepxanh.com/may-giat-bosch-8-kg-wgg234e0sg.html"> <span class="name">Bosch WGG234E0SG</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Phụ kiện bếp" img="1662"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
<ul>
 <li><a href="/gia-bat-co-dinh-tu-tren.html"> <span class="name">Kệ chén cố định</span> </a></li>
 <li><a href="/gia-bat-dia-nang-ha.html"> <span class="name">Kệ chén nâng hạ</span> </a></li>
 <li><a href="/gia-de-xoong-noi-bat-dia.html"> <span class="name">Giá xoong nồi - bát đĩa tủ dưới</span> </a></li>
 <li><a href="/gia-de-gia-vi-chai-lo-dao-thot.html"> <span class="name">Kệ gia vị, dao thớt</span> </a></li>
 <li><a href="//bepxanh.com/khay-chia-muong-nia.html"> <span class="name">Khay chia muỗng nĩa</span> </a></li>
 <li><a href="/ke-goc-tu-bep.html"> <span class="name">Kệ góc tủ bếp</span> </a></li>
 <li><a href="//bepxanh.com/mam-xoay-tu-bep.html"> <span class="name">Mâm xoay tủ bếp</span> </a></li>
 <li><a href="/tu-dung-do-kho.html"> <span class="name">Tủ đựng đồ khô</span> </a></li>
 <li><a href="/thung-gao-thong-minh.html"> <span class="name">Thùng gạo thông minh</span> </a></li>
 <li><a href="/thung-rac.html"> <span class="name">Thùng rác âm tủ</span> </a></li>
 <li><a href="/ke-dung-chai-lo-tay-rua.html"> <span class="name">Kệ đựng chai lọ tẩy rửa</span> </a></li>
 <li><a href="/ke-treo-nha-bep-da-nang.html"> <span class="name">Kệ treo nhà bếp đa năng</span> </a></li>
 <li><a href="/phu-kien-phong-ngu.html"> <span class="name">Phụ kiện phòng ngủ</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Gia dụng bếp" img="1664"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
<ul>
 <li><a href="//bepxanh.com/xoong-noi.html"> <span class="name">Xoong nồi</span> </a></li>
 <li><a href="/chao.html"> <span class="name">Chảo</span> </a></li>
 <li><a href="/bo-dao.html"> <span class="name">Bộ dao</span> </a></li>
 <li><a href="/noi-chien-khong-dau.html"> <span class="name">Nồi chiên không dầu</span> </a></li>
 <li><a href="/binh-dun-nu.html"> <span class="name">Bình đun nước</span> </a></li>
 <li><a href="/ban-ui.html"> <span class="name">Bàn ủi</span> </a></li>
 <li><a href="/vien-rua-chen.html"> <span class="name">Viên rửa chén</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
[giuseart_tab title="Thiết bị vệ sinh" img="1665"]
 
[row_inner style="small"]
 
[col_inner span__sm="12"]
<h3>Hãng điện thoại</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1640" pos="center" link="/malloca"]
 
Malloca
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo nhu cầu</h3>
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span="3" span__sm="3"]
 
[featured_box img="1641" pos="center" link="/Ecalite"]
 
Ecalite
 
[/featured_box]
 
[/col_inner]
[col_inner span__sm="12"]
<h3>Chọn theo số vùng nấu</h3>
<ul>
 <li><a href="/bep-don.html"> <span class="name">Bếp điện từ đơn </span> </a></li>
 <li><a href="/bep-2-vung-nau.html"> <span class="name">2 Vùng</span> </a></li>
 <li><a href="bep-3-vung-nau.html"> <span class="name">3 Vùng</span> </a></li>
 <li><a href="/bep-4-vung-nau.html"> <span class="name">4 Vùng</span> </a></li>
 <li><a href="/bep-tu-domino.html"> <span class="name">Bếp điện từ Domino</span> </a></li>
</ul>
<h3>Sản phẩm nổi bật</h3>
<ul>
 <li><a href="/bep-tu-bosch-hmh-ppi82560ms.html"> <span class="name">Bosch PPI82560MS</span> </a></li>
 <li><a href="/bep-tu-doi-2-vung-nau-malloca-mi-732-sl.html"> <span class="name">Malloca MI 732 SL</span> </a></li>
 <li><a href="/bep-tu-2-vung-nau-ecalite-el-ms2999ii.html"> <span class="name">Ecalite EL-MS2999II</span> </a></li>
 <li><a href="//bepxanh.com/bep-1-dien-1-tu-ecalite-el-mk2688ir.html"> <span class="name">Ecalite EL-MK2688IR</span> </a></li>
</ul>
<h3>Xuất xứ</h3>
<ul>
 <li><a> <span class="name">Tây Ban Nha</span> </a></li>
 <li><a> <span class="name">Đức</span> </a></li>
 <li><a> <span class="name">Thái Lan</span> </a></li>
 <li><a> <span class="name">Malaysia</span> </a></li>
 <li><a> <span class="name">Trung Quốc</span> </a></li>
 <li><a> <span class="name">Việt Nam</span> </a></li>
</ul>
[/col_inner]
 
[/row_inner]
 
[/giuseart_tab]
 
[/giuseart_tabs]
 
[/col]
 
[/row]

#### Trang tri class

.off-canvas-right .mfp-content, .off-canvas-left .mfp-content { width: 100%; } .off-canvas .sidebar-menu { padding: 0; } .header-block .col { padding-left: 0; padding-right: 0;padding-bottom: 0; } .giuseart_tabs { display: block; } .giuseart_tabs .nav { gap: 0; float: left; width: 18%; background-color: #fee2e1; overflow: auto; margin: 0 !important; } .giuseart_tabs ul li { padding-left: 0; } .giuseart_tabs .nav li:first-child { background: #fcb4b5; } .off-canvas .nav-vertical>li>a { padding-bottom: 10px; padding-top: 10px; font-size: 16px; text-transform: none; letter-spacing: 0; color: #333; font-weight: 500; } .giuseart_tabs ul li a img { width: 40px; height: 40px; border-radius: 99%; margin: 0 auto 5px auto; } .giuseart_tabs ul li a h3 { font-size: 14px; font-weight: 500; margin-bottom: 0; } .giuseart_tabs .nav li:nth-child(2) { background: #fee2e1; } .giuseart_tabs .nav li:nth-child(3) { background: #ffeed6; } .giuseart_tabs .nav li:nth-child(4) { background: #fff8c4; } .giuseart_tabs .nav li:nth-child(5) { background: #ecfccb; } .giuseart_tabs .nav li:nth-child(6) { background: #d1fbe5; } .giuseart_tabs .nav li:nth-child(7) { background: #e0f2fe; } .giuseart_tabs .nav li:nth-child(8) { background: #e1e7fd; } .giuseart_tabs .nav li:nth-child(9) { background: #edeaff; } .giuseart_tabs .nav li:nth-child(10) { background: #eafff9; } .giuseart_tabs .tab-panels { width: 100%; padding: 15px 10px 10px 20%; } .tab-panels .entry-content .row { margin-left: -5px !important; margin-right: -5px !important; } .giuseart_tabs .tab-panels .col { padding: 0 5px 0px !important; } .giuseart_tabs .col:first-child h3 { margin-top: 0 !important; border-left: none; padding-left: 0;line-height: 24px; font-size: 16px;margin-bottom: 10px; color: #333; } .giuseart_tabs .tab-panels .icon-box { border: solid 1px #d2d2d2; padding: 5px; border-radius: 10px; background: white; margin-bottom: 10px; } .giuseart_tabs .tab-panels .icon-box .icon-box-img { margin-bottom: 7px; width: 45px !important; } .giuseart_tabs .tab-panels .icon-box .icon-box-img img { border-radius: 10px; }.giuseart_tabs .tab-panels .icon-box .icon-box-text { padding-left: 0;color: white; font-size: 14px; line-height: 20px; }.giuseart_tabs .tab-panels ul { display: inline-block; margin-top: 0 !important; margin-bottom: 0; } .giuseart_tabs .tab-panels ul li { margin-right: 6px; display: inline-block; float: left; width: auto !important; }.giuseart_tabs .tab-panels ul li a { color: #565656; border: 1px solid #cccccc; border-radius: 10px; padding: 9px 10px; line-height: 44px; }
