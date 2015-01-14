#######################
相容性函數
#######################

CodeIgniter 提供一組相容性函數，使你可以使用非原生可使用的 PHP 函數，
但是只有在更高的版本或者依賴於一定的擴充插件。

作為客製化實作，這些函數對他們本身來說，也將有一些依賴性設定，
如果你的 PHP 安裝沒有提供原生的函數，這個方法仍然是有用的。

.. note:: 大部份像是 `通用函數 <common_functions>` ，只要依賴條件滿足，相容性函數總是可以使用的。

.. contents::
  :local:

.. raw:: html

  <div class="custom-index container"></div>

****************
密碼雜湊
****************

這組相容性函數提供一個“backport”在 PHP 的標準
 `Password Hashing extension <http://php.net/password>`_ ，
其他方式可以使用，就是將 PHP 版本升級到 PHP 5.5 。

依賴
============

- PHP 5.3.7
- ``CRYPT_BLOWFISH`` 提供給 ``crypt()``

常數
=========

- ``PASSWORD_BCRYPT``
- ``PASSWORD_DEFAULT``

函數參考
==================

.. function:: password_get_info($hash)

	:param	string	$hash: 雜湊的密碼
	:returns:	雜湊密碼的資訊
	:rtype:	array

	要獲得更多資訊，請參考 `PHP manual for
	password_get_info() <http://php.net/password_get_info>`_.

.. function:: password_hash($password, $algo[, $options = array()])

	:param	string	$password: 明文密碼
	:param	int	$algo: 雜湊演算法
	:param	array	$options: 雜湊選項
	:returns:	雜湊密碼，或者錯誤 FALSE
	:rtype:	string

	要獲得更多資訊，請參考 `PHP manual for
	password_hash() <http://php.net/password_hash>`_.

	.. note:: 除非你提供你自己的（以及有效的）salt，這個函數可以進一步提供依賴於可使用的 CSPRNG source。
	 	滿足下列每一個條件：
		- ``mcrypt_create_iv()`` with ``MCRYPT_DEV_URANDOM``
		- ``openssl_random_pseudo_bytes()``
		- /dev/arandom
		- /dev/urandom

.. function:: password_needs_rehash($hash, $algo [, $options = array()])

	:param	string	$hash: 雜湊密碼
	:param	int	$algo: 雜湊演算法
	:param	array	$options: 雜湊選項
	:returns:	TRUE 如果雜湊可以被匹配於輸入的演算法以及選項給重新雜湊，否則 FALSE
	:rtype:	bool

	要獲得更多資訊，請參考 `PHP manual for
	password_needs_rehash() <http://php.net/password_needs_rehash>`_.

.. function:: password_verify($password, $hash)

	:param	string	$password: 純文本密碼
	:param	string	$hash: 雜湊密碼
	:returns:	TRUE 如果密碼匹配雜湊，如果不是 FALSE
	:rtype:	bool

	要獲得更多資訊，請參考 `PHP manual for
	password_verify() <http://php.net/password_verify>`_.

*********************
Hash (Message Digest)
*********************

This compatibility layer contains backports for the ``hash_equals()``
and ``hash_pbkdf2()`` functions, which otherwise require PHP 5.6 and/or
PHP 5.5 respectively.

Dependencies
============

- None

Function reference
==================

.. function:: hash_equals($known_string, $user_string)

	:param	string	$known_string: Known string
	:param	string	$user_string: User-supplied string
	:returns:	TRUE if the strings match, FALSE otherwise
	:rtype:	string

	For more information, please refer to the `PHP manual for
	hash_equals() <http://php.net/hash_equals>`_.

.. function:: hash_pbkdf2($algo, $password, $salt, $iterations[, $length = 0[, $raw_output = FALSE]])

	:param	string	$algo: Hashing algorithm
	:param	string	$password: Password
	:param	string	$salt: Hash salt
	:param	int	$iterations: Number of iterations to perform during derivation
	:param	int	$length: Output string length
	:param	bool	$raw_output: Whether to return raw binary data
	:returns:	Password-derived key or FALSE on failure
	:rtype:	string

	For more information, please refer to the `PHP manual for
	hash_pbkdf2() <http://php.net/hash_pbkdf2>`_.

****************
Multibyte String
****************

This set of compatibility functions offers limited support for PHP's
`Multibyte String extension <http://php.net/mbstring>`_. Because of
the limited alternative solutions, only a few functions are available.

.. note:: When a character set parameter is ommited,
	``$config['charset']`` will be used.

Dependencies
============

- `iconv <http://php.net/iconv>`_ extension

.. important:: This dependency is optional and these functions will
	always be declared. If iconv is not available, they WILL
	fall-back to their non-mbstring versions.

.. important:: Where a character set is supplied, it must be
	supported by iconv and in a format that it recognizes.

.. note:: For you own dependency check on the actual mbstring
	extension, use the ``MB_ENABLED`` constant.

Function reference
==================

.. function:: mb_strlen($str[, $encoding = NULL])

	:param	string	$str: Input string
	:param	string	$encoding: Character set
	:returns:	Number of characters in the input string or FALSE on failure
	:rtype:	string

	For more information, please refer to the `PHP manual for
	mb_strlen() <http://php.net/mb_strlen>`_.

.. function:: mb_strpos($haystack, $needle[, $offset = 0[, $encoding = NULL]])

	:param	string	$haystack: String to search in
	:param	string	$needle: Part of string to search for
	:param	int	$offset: Search offset
	:param	string	$encoding: Character set
	:returns:	Numeric character position of where $needle was found or FALSE if not found
	:rtype:	mixed

	For more information, please refer to the `PHP manual for
	mb_strpos() <http://php.net/mb_strpos>`_.

.. function:: mb_substr($str, $start[, $length = NULL[, $encoding = NULL]])

	:param	string	$str: Input string
	:param	int	$start: Position of first character
	:param	int	$length: Maximum number of characters
	:param	string	$encoding: Character set
	:returns:	Portion of $str specified by $start and $length or FALSE on failure
	:rtype:	string

	For more information, please refer to the `PHP manual for
	mb_substr() <http://php.net/mb_substr>`_.

******************
Standard Functions
******************

This set of compatibility functions offers support for a few
standard functions in PHP that otherwise require a newer PHP version.

Dependencies
============

- None

Function reference
==================

.. function:: array_column(array $array, $column_key[, $index_key = NULL])

	:param	array	$array: Array to fetch results from
	:param	mixed	$column_key: Key of the column to return values from
	:param	mixed	$index_key: Key to use for the returned values
	:returns:	An array of values representing a single column from the input array
	:rtype:	array

	For more information, please refer to the `PHP manual for
	array_column() <http://php.net/array_column>`_.

.. function:: array_replace(array $array1[, ...])

	:param	array	$array1: Array in which to replace elements
	:param	array	...: Array (or multiple ones) from which to extract elements
	:returns:	Modified array
	:rtype:	array

	For more information, please refer to the `PHP manual for
	array_replace() <http://php.net/array_replace>`_.

.. function:: array_replace_recursive(array $array1[, ...])

	:param	array	$array1: Array in which to replace elements
	:param	array	...: Array (or multiple ones) from which to extract elements
	:returns:	Modified array
	:rtype:	array

	For more information, please refer to the `PHP manual for
	array_replace_recursive() <http://php.net/array_replace_recursive>`_.

	.. important:: Only PHP's native function can detect endless recursion.
		Unless you are running PHP 5.3+, be careful with references!

.. function:: hex2bin($data)

	:param	array	$data: Hexadecimal representation of data
	:returns:	Binary representation of the given data
	:rtype:	string

	For more information, please refer to the `PHP manual for hex2bin()
	<http://php.net/hex2bin>`_.

.. function:: quoted_printable_encode($str)

	:param	string	$str: Input string
	:returns:	8bit-encoded string
	:rtype:	string

	For more information, please refer to the `PHP manual for
	quoted_printable_encode() <http://php.net/quoted_printable_encode>`_.