# Laboratorios-Analisis-de-Datos

-- phpMyAdmin SQL Dump
-- version 5.2.1
-- https://www.phpmyadmin.net/
--
-- Servidor: 127.0.0.1
-- Tiempo de generación: 07-11-2024 a las 16:03:31
-- Versión del servidor: 10.4.32-MariaDB
-- Versión de PHP: 8.2.12

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Base de datos: `biblioteca`
--

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `autores`
--

CREATE TABLE `autores` (
  `ID_Autor` int(11) NOT NULL,
  `Nombre` varchar(100) NOT NULL,
  `Nacionalidad` varchar(50) DEFAULT NULL,
  `Fecha_de_Nacimiento` varchar(30) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Volcado de datos para la tabla `autores`
--

INSERT INTO `autores` (`ID_Autor`, `Nombre`, `Nacionalidad`, `Fecha_de_Nacimiento`) VALUES
(1, 'Gabriel_García_Márquez', 'Colombiano', '1927-03-06'),
(2, 'J.K._Rowling', 'Britanica', '1965-07-31'),
(3, 'George_Orwell', 'Britanico', '1903-06-25');

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `categorias`
--

CREATE TABLE `categorias` (
  `ID_Categoría` int(11) NOT NULL,
  `Nombre_Categoría` varchar(50) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Volcado de datos para la tabla `categorias`
--

INSERT INTO `categorias` (`ID_Categoría`, `Nombre_Categoría`) VALUES
(1, 'Novela'),
(2, 'Ciencia_Ficción'),
(3, 'Fantasia'),
(4, 'Ensayo');

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `libros`
--

CREATE TABLE `libros` (
  `ID_Libro` int(11) NOT NULL,
  `Titulo` varchar(50) NOT NULL,
  `ID_Autor` int(11) DEFAULT NULL,
  `ID_Categoría` int(11) DEFAULT NULL,
  `Año_Publicación` year(4) DEFAULT NULL,
  `Disponible` tinyint(1) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Volcado de datos para la tabla `libros`
--

INSERT INTO `libros` (`ID_Libro`, `Titulo`, `ID_Autor`, `ID_Categoría`, `Año_Publicación`, `Disponible`) VALUES
(1, 'Cien_Años_de_Soledad', 1, 1, '1967', 1),
(2, 'Harry_Potter_y_la_Piedra_Filosofal', 2, 3, '1997', 1),
(3, 'La_Era-1984', 3, 2, '1949', 1);

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `préstamos`
--

CREATE TABLE `préstamos` (
  `ID_Préstamo` int(11) NOT NULL,
  `ID_Usuario` int(11) DEFAULT NULL,
  `ID_Libro` int(11) DEFAULT NULL,
  `Fecha_Préstamo` date DEFAULT NULL,
  `Fecha_Devolución` date DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Volcado de datos para la tabla `préstamos`
--

INSERT INTO `préstamos` (`ID_Préstamo`, `ID_Usuario`, `ID_Libro`, `Fecha_Préstamo`, `Fecha_Devolución`) VALUES
(1, 1, 1, '2024-08-01', '2024-08-15'),
(2, 2, 2, '2024-08-02', '2024-08-16');

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `préstamos_usuarios`
--

CREATE TABLE `préstamos_usuarios` (
  `ID_Préstamo` int(11) NOT NULL DEFAULT 0,
  `Nombre_Usuario` varchar(50) NOT NULL,
  `Titulo_Libro` varchar(50) NOT NULL,
  `Fecha_Préstamo` date DEFAULT NULL,
  `Fecha_Devolución` date DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Volcado de datos para la tabla `préstamos_usuarios`
--

INSERT INTO `préstamos_usuarios` (`ID_Préstamo`, `Nombre_Usuario`, `Titulo_Libro`, `Fecha_Préstamo`, `Fecha_Devolución`) VALUES
(1, 'Carlos_Martinez', 'Cien_Años_de_Soledad', '2024-08-01', '2024-08-15'),
(2, 'Lucia_Fernandez', 'Harry_Potter_y_la_Piedra_Filosofal', '2024-08-02', '2024-08-16');

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `usuarios`
--

CREATE TABLE `usuarios` (
  `ID_Usuario` int(11) NOT NULL,
  `Nombre` varchar(50) NOT NULL,
  `Dirección` varchar(50) DEFAULT NULL,
  `Teléfono` varchar(13) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Volcado de datos para la tabla `usuarios`
--

INSERT INTO `usuarios` (`ID_Usuario`, `Nombre`, `Dirección`, `Teléfono`) VALUES
(1, 'Carlos_Martinez', 'Calle_Luna_123', '123456789'),
(2, 'Lucia_Fernandez', 'Aven_Sol_456', '987654321');

--
-- Índices para tablas volcadas
--

--
-- Indices de la tabla `autores`
--
ALTER TABLE `autores`
  ADD PRIMARY KEY (`ID_Autor`);

--
-- Indices de la tabla `categorias`
--
ALTER TABLE `categorias`
  ADD PRIMARY KEY (`ID_Categoría`);

--
-- Indices de la tabla `libros`
--
ALTER TABLE `libros`
  ADD PRIMARY KEY (`ID_Libro`),
  ADD KEY `ID_Autor` (`ID_Autor`),
  ADD KEY `ID_Categoría` (`ID_Categoría`);

--
-- Indices de la tabla `préstamos`
--
ALTER TABLE `préstamos`
  ADD PRIMARY KEY (`ID_Préstamo`),
  ADD KEY `ID_Usuario` (`ID_Usuario`),
  ADD KEY `ID_Libro` (`ID_Libro`);

--
-- Indices de la tabla `usuarios`
--
ALTER TABLE `usuarios`
  ADD PRIMARY KEY (`ID_Usuario`);

--
-- AUTO_INCREMENT de las tablas volcadas
--

--
-- AUTO_INCREMENT de la tabla `autores`
--
ALTER TABLE `autores`
  MODIFY `ID_Autor` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=4;

--
-- AUTO_INCREMENT de la tabla `categorias`
--
ALTER TABLE `categorias`
  MODIFY `ID_Categoría` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=5;

--
-- AUTO_INCREMENT de la tabla `libros`
--
ALTER TABLE `libros`
  MODIFY `ID_Libro` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=4;

--
-- AUTO_INCREMENT de la tabla `préstamos`
--
ALTER TABLE `préstamos`
  MODIFY `ID_Préstamo` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=3;

--
-- AUTO_INCREMENT de la tabla `usuarios`
--
ALTER TABLE `usuarios`
  MODIFY `ID_Usuario` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=3;

--
-- Restricciones para tablas volcadas
--

--
-- Filtros para la tabla `libros`
--
ALTER TABLE `libros`
  ADD CONSTRAINT `libros_ibfk_1` FOREIGN KEY (`ID_Autor`) REFERENCES `autores` (`ID_Autor`),
  ADD CONSTRAINT `libros_ibfk_2` FOREIGN KEY (`ID_Categoría`) REFERENCES `categorias` (`ID_Categoría`);

--
-- Filtros para la tabla `préstamos`
--
ALTER TABLE `préstamos`
  ADD CONSTRAINT `préstamos_ibfk_1` FOREIGN KEY (`ID_Usuario`) REFERENCES `usuarios` (`ID_Usuario`),
  ADD CONSTRAINT `préstamos_ibfk_2` FOREIGN KEY (`ID_Libro`) REFERENCES `libros` (`ID_Libro`);
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
